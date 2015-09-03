{% import './data.html' as data %}

# Report

As a class, we brainstormed and came up with a long list of further questions we can ask based
on the "self-introduction" data. Out of these questions, our team chose to tackle on
the following:

# How many people are in the CS department?

{% lodash %}
var x = _.filter(data.comments, function(n){
return _.includes(n.body, "Computer Science") || _.includes(n.body, "CS");})
return _.size(x)
{% endlodash %}

There are {{result}} people in the Computer Science department.


# How many people have names that start with "A"?

{% lodash %}
var list = _.filter(_.pluck(data.comments, "body"), function(text){
var a = text.split("\r\n")[0]
var name = _.last(text.split("Name:"))
return name.charAt(1) == "A"
})
return _.size(list)
{% endlodash %}

There are {{result}} people whose names start with "A".
#How many students are not CS majors?

{% lodash %}
var x = _.filter(data.comments, function(n){
return _.includes(n.body, "Computer Science") || _.includes(n.body, "CS");})
return data.comments.length - _.size(x)
{% endlodash %}

There are {{result}} people who are not in the Computer Science department.

# What is the ID number of user: Zhya215?
{% lodash %}
var x = _.filter(data.comments, function(n){
return _.includes(n.user, "zhya215");
})

var y = _.pluck(x, "user.id")
return y
{% endlodash %}

Zhya215 has an ID number of {{result}}.
