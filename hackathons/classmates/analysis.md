# Analysis

{% import './data.html' as data %}

After completing the warmup exercises, your task is to do four more slightly
more challenges analyses.

## How many students like sushi as their favorite food?

{% lodash %}

var x = _.filter(data.comments, function(n){
return _.includes(n.body, "Sushi");})
return _.size(x)

{% endlodash %}

The answer is {{result}}.

## Who are the students liking Python the most?

{% lodash %}
var x = _.filter(data.comments, function(n){
return _.includes(n.body, "Python");
})

var y = _.pluck(x, "body")
var nameArray = []
var finalNameArray = []

for (i = 0; i < _.size(y); i ++){
nameArray.push(_.first(y[i].split("\r\n")))
finalNameArray.push(_.last(nameArray[i].split("Name:")))
}

return finalNameArray
{% endlodash %}

Their names are {{result}}.

## Are there more Javascript lovers or Java lovers?

{% lodash %}
var x = _.filter(data.comments, function(n){
return _.includes(n.body, "Java");})
var javaSize = _.size(x)

var y = _.filter(data.comments, function(n){
return _.includes(n.body, "JavaScript");})
var jscriptSize = _.size(y)
if (javaSize > jscriptSize)
return "Java"
else
return "JavaScript"
{% endlodash %}

The answer is {{result}}.

## Who like the same food as `kjblakemore`?

{% lodash %}
var x = _.filter(data.comments, function(n){
return _.includes(n.body, "Vegan");
})

var y = _.pluck(x, "body")
var nameArray = []
var finalNameArray = []

for (i = 0; i < _.size(y); i ++){
nameArray.push(_.first(y[i].split("\r\n")))
finalNameArray.push(_.last(nameArray[i].split("Name:")))
}

return finalNameArray
{% endlodash %}

Their names are {{result}}.
