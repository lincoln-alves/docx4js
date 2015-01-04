#docx4js
a javascript docx parser

#install
	$ npm install docx4js

#API
```html
	<script src="../dist/docx4js.js"></script>
	<script>
		var Text=(function(){
			var converter=[]
			converter.visit=function(){
				if(this.model.type=='paragraph')
					return this.push("\n\r")
				if(this.model.type=='text')
					return this.push(this.model.getText())
			}
			
			function factory(model, doc, parent){
				converter.model=model
				return converter
			}
			
			factory.with=function(parent){
				return factory
			}
			
			factory.asResult=function(){
				return converter.join('')
			}
			
			return factory
		})();
		function test(input){
			require('docx4js').load(input.files[0])
				.then(function(doc){
					input.value=""
					document.$1('body>pre').innerHTML=""
					doc.parse(Text)
					document.$1('body>pre').innerHTML=(Text.asResult())
				})
		}
	</script>
	<body>
		<input type="file" style="position:absolute;top:0" onchange="test(this)">
		<pre></pre>
	</body>
```

