# Timing for building PLUMED-TUTORIALS lessons

{% assign xx="" %}
{% assign yy="" %}

{% for item in site.data.lessons %}
 {% assign xx=xx | append: item.id  | append: ", " %}
 {% assign t = item.time | plus: 0 %}
 {% assign yy=yy | append: t | append: ", " %}
{% endfor %}

{{ xx }}
{{ yy }}

The chart below shows the time needed to build each lesson in PLUMED-TUTORIALS.

<canvas id="myChart" style="width:100%;"></canvas>

<script>
var xValues = [ {{ xx | split: ',' }} ];
var yValues = [ {{ yy | split: ',' }} ];
// do sorting in descending order based on yValues
//1) combine the arrays:
var list = [];
for (var j = 0; j < xValues.length; j++) 
    list.push({'x': xValues[j], 'y': yValues[j]});
//2) sort:
list.sort(function(a, b) {
    return ((a.y > b.y) ? -1 : ((a.y == b.y) ? 0 : 1));
});
//3) separate them back out:
for (var k = 0; k < list.length; k++) {
    xValues[k] = list[k].x;
    yValues[k] = list[k].y;
} 
var barColors = "green";

new Chart("myChart", {
  type: "horizontalBar",
  data: {
    labels: xValues,
    datasets: [{
      backgroundColor: barColors,
      data: yValues
    }]
  },
  options: {
    maintainAspectRatio: false,
    legend: {display: false},
    title: {
      display: true,
      text: "Build time (s)"
    }
  }
});
</script>