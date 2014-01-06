var express = require('express');
var app = express();
var fs =  require('fs');

var PORT = 3000;

var STATIC_DIR = '../content/';
var MIME_HTML = 'text/html';

var EDITOR_FILE = 'editor.html';
var EDITOR_PATH = '/';

var LOAD_PATH = '/load';
var SAVE_PATH = '/save';

var CONTENT_TYPE = 'Content-Type';
var CONTENT_LENGTH = 'Content-Length';

app.use(express.bodyParser());

app.get(EDITOR_PATH, function(req, res) {
	res.setHeader(CONTENT_TYPE, MIME_HTML);
	fs.readFile(EDITOR_FILE, function read(err, data) {
		if (err) {
			console.log(err);
		}
		res.setHeader(CONTENT_LENGTH, data.length);
		res.end(data);
	})
});

app.get(LOAD_PATH, function(req, res){
  	var fileName = req.query.fileName;
	res.setHeader(CONTENT_TYPE, MIME_HTML);
	fs.readFile(STATIC_DIR + fileName, function read(err, data) {
	    if (err) {
	        console.log(err);
		var body = "Could not read content. Please check file-name is correct.";
		res.setHeader(CONTENT_LENGTH, body.length);
		res.end(body);
	    } else {
		console.log(fileName);	   
		res.setHeader(CONTENT_LENGTH, data.length);
		res.end(data);
	    }
	});
});

app.post(SAVE_PATH, function(req, res) {
	var fileName = req.param('fileName');
	var content = req.param('content');
	console.log("Filename is: " + fileName);	
	console.log("Content is: " + content);
	fs.writeFile(STATIC_DIR + fileName, content, function(err) {
		if(err) {
        		console.log(err);
		} else {	
	        	console.log("The file was saved!");
		}
	});
	var body = "OK";
	res.setHeader(CONTENT_TYPE, 'text/plain');
	res.setHeader(CONTENT_LENGTH, body.length);
	res.end(body);
});

app.listen(PORT);
console.log('Listening on port ' + PORT);
