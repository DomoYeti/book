{% data src="fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.

# Which department has the highest enrollment? by Tristan Wagar

{% lodash %}
var groups = _.groupBy(data, function(college){
return college["Subject"]
})
var courseEnroll = _.mapValues(groups, function(a){
return _.map(a, function(b){
return b["N"]["ENROLL"]
})
})
var enroll = _.mapValues(courseEnroll, function(enrolls){
return _.sum(enrolls)
})
return _.pick(enroll, function(number){
return number == _.max(enroll)
})

{% endlodash %}
<table>
{% for key, value in result %}
<tr>
<td> {{key}}</td>
<td>{{value}}</td>
</tr>
{% endfor %}
</table>

# Which instructor's course has the highest enrollment? by Zhili Yang

{% lodash %}
var list = _.map(data, function(course){
var instructors = course["Instructors"]
var enroll = course["N"]["ENROLL"]
var courseName = course["CourseTitle"]
return _.map(instructors, function(instructor){
return {"instructor": instructor["name"], "courseTitle": courseName, "enrollment": enroll}
})
})

var maxGroups = _.max(_.flatten(list), function(course){
return course["enrollment"]
})
return maxGroups
{% endlodash %}

The professor is {{result["instructor"]}}.

# How many courses in IPHY that has 4 credit hours? by Fadhil Fath

{% lodash %}
var course = _.filter(data, function(n){
return n["CrsPBADept"] == "IPHY"
})

var hour = _.filter(course, function(d){
return d["Hours"] == 4
})

return _.size(hour)

{% endlodash %}

There are {{result}} courses in IPHY with 4 credit hours.

# Which department offers the most 4000 level classes? by Brian McKean

{% lodash %}
var groups = _.groupBy(data, function(college){
return college["Subject"]
})

var courseLevels = _.mapValues(groups, function(a){
return _.map(a, function(b){
return b["Course"]
})
})
var count = 0
var levelCount = _.mapValues(courseLevels, function(level){
count = 0
return _.map(level, function(n){
if(n >= 4000 && n < 5000){
count ++
}
return count
})
})

var result = _.mapValues(levelCount, function(n){
return _.max(n)
})
return _.pick(result, function(number){
return number == _.max(result)
})
{% endlodash %}

<table>
{% for key, value in result %}
<tr>
<td> {{key}}</td>
<td>{{value}}</td>
</tr>
{% endfor %}
</table>

# What instructor has the highest rating? by Andrew Krodinger

{% lodash %}
var list = _.map(data, function(course){
var instructors = course["Instructors"]
var enroll = course["AvgInstructor"]
return _.map(instructors, function(instructor){
return {"instructor": instructor["name"], "rating": enroll}
})
})

var maxGroups = _.max(_.flatten(list), function(course){
return course["rating"]
})
return maxGroups
{% endlodash %}

<table>
{% for key, value in result %}
<tr>
<td> {{key}}</td>
<td>{{value}}</td>
</tr>
{% endfor %}
</table>
