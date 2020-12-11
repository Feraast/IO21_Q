# IO21
Interview question (IO21):

ML Facial Detection

Application Server: Node JS
Middleware: Express
Backend: MongoDB
Machine Learning Library: "node-red-contrib-face-recognition" node in Node-Red

To run this, you need to install Node Red, which is where the ML portion is taking place. After installation, you need to go to localhost:1880 on the browser and import the flow below (copy paste). After deploying the flow shown below, you can run app.js in this repo from VS Code or any other IDE normally.

[{"id":"df046a5b.f02238","type":"tab","label":"Lab 11 Ex.5 ","disabled":false,"info":""},{"id":"2ca68c92.218134","type":"change","z":"df046a5b.f02238","name":"Set Payload to Image","rules":[{"t":"set","p":"payload","pt":"msg","to":"payload[\"TBB Faces\"].image","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":780,"y":320,"wires":[[]]},{"id":"6d846a1c.618f14","type":"base64","z":"df046a5b.f02238","name":"","action":"","property":"payload","x":200,"y":360,"wires":[[]]},{"id":"e3a75145.27873","type":"face-api-input","z":"df046a5b.f02238","name":"Find Faces","numNodes":1,"computeNode1":"5adfec11.8f4ef4","computeNode2":"","computeNode3":"","computeNode4":"","computeNode5":"","computeNode6":"","computeNode7":"","computeNode8":"","computeNode9":"","computeNode10":"","x":530,"y":240,"wires":[["2ca68c92.218134","15d72e2a.2e9d32","9e519d8f.8f35b"]]},{"id":"122d5539.0a253b","type":"function","z":"df046a5b.f02238","name":"Save Res","func":"// msg.payload = {\"Expression\": msg.payload[\"TBB Faces\"].faces[0].expressionLabel\n//                 , \"Image\": msg.payload[\"TBB Faces\"].image\n            \n// }\n\n// return msg\n\nflow.set(\"response\",msg.res);\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","x":440,"y":120,"wires":[["4942da23.90c174"]]},{"id":"6d178739.cedf78","type":"debug","z":"df046a5b.f02238","name":"FunctionDebug","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":1170,"y":160,"wires":[]},{"id":"48b8ee6f.bb4ee","type":"http response","z":"df046a5b.f02238","name":"HTTP Response","statusCode":"200","headers":{},"x":1120,"y":320,"wires":[]},{"id":"49cdfad9.7b3494","type":"http in","z":"df046a5b.f02238","name":"","url":"/expression","method":"get","upload":false,"swaggerDoc":"","x":220,"y":120,"wires":[["122d5539.0a253b"]]},{"id":"15d72e2a.2e9d32","type":"function","z":"df046a5b.f02238","name":"Get Res","func":"msg.payload = {\"expression\": msg.payload[\"TBB Faces\"].faces[0].expressionLabel,\n                \"gender\": msg.payload[\"TBB Faces\"].faces[0].gender,\n                \"age\": msg.payload[\"TBB Faces\"].faces[0].age,\n                \n                \"image\": 'data:image/png;base64,' + msg.payload[\"TBB Faces\"].image.toString('base64')\n}\n\nmsg.res = flow.get(\"response\");\n\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","x":760,"y":200,"wires":[["6d178739.cedf78","cb3dbb63.23aa48"]]},{"id":"4df8da24.7648d4","type":"inject","z":"df046a5b.f02238","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":140,"y":240,"wires":[["4942da23.90c174"]]},{"id":"4942da23.90c174","type":"http request","z":"df046a5b.f02238","name":"","method":"GET","ret":"bin","paytoqs":"query","url":"localhost:1234/result","tls":"","persist":false,"proxy":"","authType":"","x":320,"y":240,"wires":[["e3a75145.27873","6d846a1c.618f14"]]},{"id":"cb3dbb63.23aa48","type":"template","z":"df046a5b.f02238","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"<html>\n    <p>Your expression is: {{payload.expression}}</p>\n    <p>your gender is: {{payload.gender}} </p>\n    <p>Your age is: {{payload.age}} </p>\n    <img width=\"200\" height=\"200\" src={{payload.image}}>\n</html>","output":"str","x":1000,"y":240,"wires":[["48b8ee6f.bb4ee"]]},{"id":"9e519d8f.8f35b","type":"debug","z":"df046a5b.f02238","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":640,"y":400,"wires":[]},{"id":"5adfec11.8f4ef4","type":"face-api-compute","name":"TBB Faces","childHost":true,"recognitionType":"SSD","multipleFaces":"Multiple Faces","confidence":"50","inputSize":"416","landmarks":true,"expressions":true,"ageGender":true,"recognition":false,"labelName":"known","file":""}]

