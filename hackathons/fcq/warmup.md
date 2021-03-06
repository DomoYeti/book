{% data src="fcq.clean.json" %}
{% enddata %}

# Warmup

Next, complete the following warmup exercises as a team.

## How many unique subject codes?

{% lodash %}
var subjectCodes = _.pluck(data, 'Subject')
var result = _.uniq(subjectCodes)
return _.size(result)
{% endlodash %}

There are {{ result }} unique subject codes.

## How many computer science (CSCI) courses?

{% lodash %}
var subjectCodes = _.pluck(data, 'Subject')
var result = _.filter(subjectCodes, function(n){
return n == 'CSCI'
})
return _.size(result)
{% endlodash %}

There are {{ result }} computer science courses.

## What is the distribution of the courses across subject codes?

{% lodash %}
var groups = _.groupBy(data, function(n){
return n.Subject
})
var result = _.mapValues(groups, function(n){
return n.length
})
return result
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 100 courses?

{% lodash %}
var groups = _.groupBy(data, function(n){
return n.Subject
})
var maps = _.mapValues(groups, function(n){
return n.length
})
var result = _.pick(maps, function (a){
return a > 100
})
return result
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 5000 total enrollments?

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
return number > 5000
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

## What are the course numbers of the courses Tom (PEI HSIU) Yeh taught?

{% lodash %}
var courses = _.filter(data, function(course){
var instructor = _.filter(course["Instructors"], function(instructor){
return instructor["name"] == "YEH, PEI HSIU"
})
return _.size(instructor) > 0
})
return _.map(courses, function(course){
return course["Course"]
})
{% endlodash %}

They are {{result}}.
