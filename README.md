NDM Javascript Code Test Solutions
==================================

1. Fix the below Javascript code so that the correct index is printed to console.log on each iteration.

  Solution:
	
	    (function() {
    		var index,
    			length = 10;
    		
    		for (index = 0; index < this.length; index++) {
    			console.log(index);
    		}
    	})();

    Notes:
    
    I solved this problem by removing the setTimeout(…) call, as this call was A) causing the console.log(…) call to occur out-of-process, so that it was called after the for-loop had finished and index had already been incremented to 18, B) unnecessary for the program to function correctly.

2. 	Modify the below JavaScript so that it is called just after the DOM has loaded. No legacy browser support required.

    Solution:

            window.onload = function () {
                document.getElementById("test").innerHTML = "Hello World";
            };

3. 	Modify the below code so that it will only display a message if the user is using Internet Explorer 7

    Solution:

        	(function() {
        		if (navigator.userAgent.indexOf('MSIE 9.0') > -1) {
        			alert("Hello World");
        		}
        	})();

4. Modify the below JavaScript code so that it uses a closure to return the response.

    Solution:

    	(function() {
    		function hello(name, age, callback) {
    			callback(name + ", who is " + age + " years old, says hi!");
    		}
    		hello('John', 33, function (returnValue) {
    			console.log(returnValue);
    		});
    	}();

    Notes:
    
    Not sure what is meant by this question, but assuming it means that the ‘hello’ function should call a callback, rather than return the value, here’s how I’d do it:

5. Finish the below JavaScript by implementing a simple flow control function (flow) that can take the provided array of functions and process them asynchronously before making a final callback.

    Solution:

    	(function() {
    		var array = [
    			function(callback) {
    				console.log("first function called in " + (new Date().getTime() - timestamp) + "ms");
    				callback();
    			},
    			function(callback) {
    				console.log("second function called in " + (new Date().getTime() - timestamp) + "ms");
    				callback();
    			},
    			function(callback) {
    				console.log("third function called in " + (new Date().getTime() - timestamp) + "ms");
    				callback();
    			}
    		],
    
    		timestamp = new Date().getTime();
    
    		function flow(array, callback) {
    			if (array.length == 0) {
    				callback();
    				return;
    			}
    			array[0](function () {
    				flow(array.slice(1), callback);
    			});
    		}
    
    		flow(array, function() {
    			console.log("all functions finished in " + (new Date().getTime() - timestamp) + "ms");
    		});
    
    	})();

6. Modify the below code so that the return value can also be returned with a callback function (if a callback function has been specified).

    Solution:

    	(function() {
    		function isArray(array, callback) {
    			var result = typeof(array) === "object" && (array instanceof Array);
    			if (callback && typeof callback === "function") {
    				callback(result);
    			}
    			return result;
    		}
    
    		var result = isArray([
    			"item1",
    			"item2",
    			"item3"
    		]);
    
    		console.log("isArray: " + result);
    	})();
    
7. Optimize the below JavaScript to minimize the number of redraws and reflows required.
        
    Solution:

        (function() { 
        	var element, 
        		index, 
        		length, 
        		content = document.getElementById("content"),
        		html = "",
        		data = [{ 
        			id: 1, 
        			name: "John", 
        			color: "green" 
        		}, { 
        			id: 2, 
        			name: "Sally", 
        			color: "pink" 
        		}, { 
        			id: 3, 
        			name: "Andrew", 
        			color: "blue" 
        		}, { 
        			id: 4, 
        			name: "Katie", 
        			color: "purple" 
        		}];
        
        	for (index = 0; index < data.length; index++) {
        		html +=
        			'<li id="' + data[index].id + '" style="color: ' + data[index].color + '">' +
        				'<strong>' + data[index].name + '</strong>' +
        			'</li>';
        	} 
        
        	content.innerHTML = html;
        })();

    Notes:
    
    Used string concatenation to build the HTML, which is then injected into the DOM once, using innerHTML. This reduces the number of DOM manipulations, and thus, the number of redraws/reflows required.
    
8. Using the below JavaScript code as a starting point, implement a chain-able DOM Wrapper API that operates in a similar fashion to jQuery's API (No native prototype  extensions).

	Solution:

		(function() {
			var $ = function (selector) {
				var elements = document.querySelectorAll("#test");
				var that = this;

				this.show = function() {
					var array = Array.prototype.slice.call(elements, 0); 
					array.forEach(function(node) {
						node.style.display = "block";
					});
					return that;
				};

				this.hide = function() {
					var array = Array.prototype.slice.call(elements, 0); 
					array.forEach(function(node) {
						node.style.display = "none";
					});
					return that;
				}

				return this;
			};

			$("#test").show().hide();
		})();
	
