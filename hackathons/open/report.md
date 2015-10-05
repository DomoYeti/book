{% data src="emergency.json" %}
{% enddata %}
# Report

Use only Javascript and SVG to produce a data analysis / visualization report.

# Authors

This report is prepared by
* [Robert Kendl](https://github.com/DomoYeti)
* [Kevin Gifford](https://github.com/KevinKGifford)
* [John Raesly](https://github.com/jraesly)

<a name="top"/>
<div id="autonav"></div>

# Which Borough has the Highest Number of Incidents?

{% lodash %}
var groups = _.groupBy(data, function(n){
return n.Borough
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

The borough with the highest number of incidents is Manhattan.

# What is the Most Common Incident?

{% lodash %}
var groups = _.groupBy(data, function(n){
return n["Incident Type"]
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

The most common incident is the Utility - Water Main.

# Which Borough has the Highest Amount of Fire-1st Alarm Incidents?

{% lodash %}
var fire = _.filter(data, function(n){
return n["Incident Type"] == "Fire-1st Alarm"
})
var groups = _.groupBy(fire, function(n){
return n.Borough
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
Manhattan is the borough with the highest amount of Fire-1st Alarm incidents.