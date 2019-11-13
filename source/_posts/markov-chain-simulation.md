---
title: 馬可夫鍊模擬 Markov Chain Simulation
date: 2016-03-19 12:16:00
tags: [程式, 模擬, ]
---

<div style="line-height: 24.0pt; text-align: justify; text-justify: inter-ideograph;">
<div style="line-height: 24pt; margin: 0cm 0cm 0.0001pt;">
<span lang="EN-US" style="font-family: , sans-serif; font-size: 13.5pt;">&#xA0; &#xA0; &#xA0; &#xA0;&#xA0;</span><span style="font-family: , sans-serif; font-size: 13.5pt;">&#x99AC;&#x53EF;&#x592B;&#x93C8;<span class="apple-converted-space"><span lang="EN-US">&#xA0;</span></span><span lang="EN-US">(Markov chain) </span>&#x6216;&#x7A31;</span><span style="font-family: , sans-serif; font-size: 13.5pt;">&#x99AC;&#x53EF;&#x592B;&#x904E;&#x7A0B;<span lang="EN-US">&#xA0;(Markov process)</span>&#x662F;&#x4E00;&#x7A2E;&#x96A8;&#x6A5F;&#x904E;&#x7A0B;&#xFF0C;&#x5728;&#x6578;&#x5B78;&#x4E0A;&#x53EA;&#x8981;&#x9019;&#x50B3;&#x905E;&#x77E9;&#x9663;&#x6709;&#x4E00;&#x4E9B;&#x597D;&#x7684;&#x6027;&#x8CEA;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x8B49;&#x660E;&#x7D93;&#x7531;&#x9019;&#x99AC;&#x53EF;&#x592B;&#x93C8;&#x62BD;&#x6A23;&#x7684;&#x5206;&#x4F48;&#x6703;&#x6536;&#x6582;&#x5230;&#x60F3;&#x8981;&#x7684;&#x6A5F;&#x7387;&#x5206;&#x4F48;&#x3002;</span></div>
<div style="line-height: 24pt; margin: 0cm 0cm 0.0001pt; text-indent: 24pt;">
<span style="font-family: , sans-serif; font-size: 13.5pt;">&#x9019;&#x908A;&#x6211;&#x7C21;&#x55AE;<span style="text-indent: 0px;">&#x6A21;&#x64EC;</span>&#x6709;&#x4E00;&#x7FA4;&#x4EBA;&#xFF0C;&#x5206;&#x70BA;<span lang="EN-US">A</span>&#x548C;<span lang="EN-US">B</span>&#x5169;&#x7A2E;&#x72C0;&#x614B;&#xFF0C;&#x4E26;&#x4E14;&#x4E00;&#x958B;&#x59CB;&#x5169;&#x7A2E;&#x72C0;&#x614B;&#x4EBA;&#x6578;&#x76F8;&#x540C;&#xFF0C;&#x800C;&#x6BCF;&#x56DE;&#x5408;&#xA0;<span lang="EN-US">A&#xA0;</span></span><span style="font-size: 18px; line-height: 24pt; text-indent: 0px;">&#x4E2D;&#x7684;&#x6BCF;&#x500B;&#x4EBA;</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">&#x6703;&#x6709;&#xA0;</span><span lang="EN-US" style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">aRate&#xA0;</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">&#x6A5F;&#x7387;&#x8B8A;&#xA0;</span><span lang="EN-US" style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">B</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">&#xFF0C;</span><span lang="EN-US" style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">B&#xA0;</span><span style="font-size: 18px; line-height: 24pt; text-indent: 0px;">&#x4E2D;&#x7684;&#x6BCF;&#x500B;&#x4EBA;</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">&#x6703;&#x6709;&#xA0;</span><span lang="EN-US" style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">bRate&#xA0;</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">&#x7684;&#x6A5F;&#x7387;&#x8B8A;&#xA0;</span><span lang="EN-US" style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">A</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">&#x3002;&#x5982;&#x6B64;&#x9032;&#x884C;&#x591A;&#x56DE;&#x5408;&#x3002;</span><span style="font-size: 13.5pt; line-height: 24pt; text-indent: 24pt;">(&#x9019;&#x662F; Agent-Based &#x800C;&#x4E0D;&#x662F;&#x76F4;&#x63A5;&#x77E9;&#x9663;&#x904B;&#x7B97;)</span></div>
<div style="line-height: 24pt; margin: 0cm 0cm 0.0001pt;">
<!-- more --> 
<a name="more"></a><span style="font-family: , sans-serif; font-size: 13.5pt;">&#x7A0B;&#x5F0F;&#x6A21;&#x64EC;&#xFF1A;<span lang="EN-US"><o:p></o:p></span></span></div>
</div>
<div style="line-height: 24.0pt; text-align: justify; text-justify: inter-ideograph;">
A to B: ( 0 ~ 1 )<br>
<input id="aRate" max="1.0" min="0.0" type="number" value="0.2"><br>
B to A: ( 0 ~ 1 )<br>
<input id="bRate" max="1.0" min="0.0" type="number" value="0.1">
<button>Result</button>
<br>
<div id="Res">
</div>
<script>
var aRate, bRate;
$(document).ready(function(){
 $("button").click(function(){
  aRate = $("#aRate").val();
  bRate = $("#bRate").val();
  f();
 });
});
var Pss = { // person state
 A: 1,
 B: 2
};
  
function f() {
    var res = System.runRounds(), data = [];
 for(var i=0; i<= System.NumRounds; i++){
  data.push({ Terms: i, A: res[i].A, B: res[i].B});
 }
 showResult(data);
}

var System = (function (){
 var People = [];
 
 var runRounds = function(){
  var result = [];  
  initialize();
  result.push({ A: System.NumPeople, B: System.NumPeople}); // initial
  for(var i= 0; i< System.NumRounds;i++){
   result.push( aRound());
  }
  return result;
 };
 
 var initialize = function(){
  People = []; 
  for(var i= 0; i< System.NumPeople; i++){
   People.push(new Person(Pss.A));
   People.push(new Person(Pss.B));
  }
 };
 
 var aRound = function(){ 
  People.forEach(function(ps){
   ps.change();
  });
  return count();
 };
 
 var count = function(){
  var Pp = People;
  var data = { A: 0, B: 0};
  for(var i in Pp){
   if(Pp[i].State == Pss.A) data.A++;
   else data.B++;
  }
  return data;
 };
 
 return{
  NumPeople: 10000,
  NumRounds: 20,
  runRounds: runRounds
 };
})();

function Person(state){
 this.State = state;
}

Person.prototype.change = function(){
 this.Rate = (this.State == Pss.A)? aRate: bRate;
 this.State = (Math.random()< this.Rate)? 3^this.State: this.State;
}

function showResult(data) {
 var margin = {top: 20, right: 20, bottom: 30, left: 40},
  width = 500 - margin.left - margin.right,
  height = 300 - margin.top - margin.bottom;

 var x0 = d3.scale.ordinal()
  .rangeRoundBands([0, width-20], .1);

 var x1 = d3.scale.ordinal();

 var y = d3.scale.linear()
  .range([height, 0]);
 
 var color = d3.scale.ordinal()
  .range([  "#aa4748","#ff8c00"]);
 
 var xAxis = d3.svg.axis()
  .scale(x0)
  .orient("bottom");
 
 var yAxis = d3.svg.axis()
  .scale(y)
  .orient("left")
  .tickFormat(d3.format(".2s"));
    $("#Res").empty();
    
 var svg = d3.select("#Res").append("svg")
  .attr("width", width + margin.left + margin.right)
  .attr("height", height + margin.top + margin.bottom)
 .append("g")
  .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

 var X_Names = ['A','B',];

 data.forEach(function(d) {
    d.xs = X_Names.map(function(name) { return {name: name, value: +d[name]}; });
 });

 x0.domain(data.map(function(d) { return d.Terms; }));
 x1.domain(X_Names).rangeRoundBands([0, x0.rangeBand()]);
 y.domain([0, d3.max(data, function(d) { return d3.max(d.xs, function(d) { return d.value; }); })]);

 svg.append("g")
  .attr("class", "x axis")
  .call(xAxis)
  .attr("transform", "translate(0," + height + ")")
  .append("text")
  .attr("x", width+10)
  .attr("y", 20)
  .style("text-anchor", "end")
  .text("Terms");;

 svg.append("g")
  .attr("class", "y axis")
  .call(yAxis)
  .append("text")
  .attr("transform", "rotate(-90)")
  .attr("y",6)
  .attr("dy", ".71em")
  .style("text-anchor", "end")
  .text("People");

 var terms = svg.selectAll(".terms")
  .data(data)
  .enter().append("g")
  .attr("class", "terms")
  .attr("transform", function(d) { return "translate(" + x0(d.Terms) + ",0)"; });

 terms.selectAll("rect")
  .data(function(d) { return d.xs; })
  .enter().append("rect")
  .attr("width", x1.rangeBand())
  .attr("x", function(d) { return x1(d.name); })
  .attr("y", function(d) { return y(d.value); })
  .attr("height", function(d) { return height - y(d.value); })
  .style("fill", function(d) { return color(d.name); });

 var legend = svg.selectAll(".legend")
  .data(X_Names.slice().reverse())
  .enter().append("g")
  .attr("class", "legend")
  .attr("transform", function(d, i) { return "translate(0," + i * 20 + ")"; });

 legend.append("rect")
  .attr("x", width - 16)
  .attr("width", 18)
  .attr("height", 18)
  .style("fill", color);

 legend.append("text")
  .attr("x", width+12 )
  .attr("y", 9)
  .attr("dy", ".35em")
  .style("text-anchor", "end")
  .text(function(d) { return d; });

};

</script>
HTML Code:</div>
<pre class="codeblock prettyprint">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;title&gt;Simulation&lt;/title&gt;
 &lt;meta charset=&quot;utf-8&quot;&gt;
 &lt;style&gt;
  body {
   font: 14px sans-serif;
  }
  .axis path,
  .axis line {
   fill: none;
   stroke: #111;
   shape-rendering: crispEdges;
  }
  .x.axis path {
   display: none;
  }
 &lt;/style&gt;
 &lt;script src=&quot;https://d3js.org/d3.v3.min.js&quot;&gt;&lt;/script&gt;
 &lt;script src=&quot;https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js&quot;&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;p&gt;Exchange System&lt;/p&gt;
&lt;p&gt;A to B: ( 0 ~ 1 )&lt;/p&gt;
&lt;input type=&quot;number&quot; id=&quot;aRate&quot; value=&apos;0.2&apos; min=&apos;0.0&apos; max=&apos;1.0&apos;&gt;
&lt;p&gt;B to A: ( 0 ~ 1 )&lt;/p&gt;
&lt;input type=&quot;number&quot; id=&quot;bRate&quot; value=&apos;0.1&apos; min=&apos;0.0&apos; max=&apos;1.0&apos;&gt;
&lt;button&gt;Result&lt;/button&gt;
&lt;div id=&quot;Res&quot;&gt;&lt;/div&gt;

&lt;script&gt;
var aRate, bRate;
$(document).ready(function(){
 $(&quot;button&quot;).click(function(){
  aRate = $(&quot;#aRate&quot;).val();
  bRate = $(&quot;#bRate&quot;).val();
  f();
 });
});
var Pss = { // person state
 A: 1,
 B: 2
};
  
function f() {
    var res = System.runRounds(), data = [];
 for(var i=0; i&lt;= System.NumRounds; i++){
  data.push({ Terms: i, A: res[i].A, B: res[i].B});
 }
 showResult(data);
}

var System = (function (){
 var People = [];
 
 var runRounds = function(){
  var result = [];  
  initialize();
  result.push({ A: System.NumPeople, B: System.NumPeople}); // initial
  for(var i= 0; i&lt; System.NumRounds;i++){
   result.push( aRound());
  }
  return result;
 };
 
 var initialize = function(){
  People = []; 
  for(var i= 0; i&lt; System.NumPeople; i++){
   People.push(new Person(Pss.A));
   People.push(new Person(Pss.B));
  }
 };
 
 var aRound = function(){ 
  People.forEach(function(ps){
   ps.change();
  });
  return count();
 };
 
 var count = function(){
  var Pp = People;
  var data = { A: 0, B: 0};
  for(var i in Pp){
   if(Pp[i].State == Pss.A) data.A++;
   else data.B++;
  }
  return data;
 };
 
 return{
  NumPeople: 10000,
  NumRounds: 30,
  runRounds: runRounds
 };
})();

function Person(state){
 this.State = state;
}

Person.prototype.change = function(){
 this.Rate = (this.State == Pss.A)? aRate: bRate;
 this.State = (Math.random()&lt; this.Rate)? 3^this.State: this.State;
}

function showResult(data) {
 var margin = {top: 20, right: 20, bottom: 30, left: 40},
  width = 900 - margin.left - margin.right,
  height = 500 - margin.top - margin.bottom;

 var x0 = d3.scale.ordinal()
  .rangeRoundBands([0, width-20], .1);

 var x1 = d3.scale.ordinal();

 var y = d3.scale.linear()
  .range([height, 0]);
 
 var color = d3.scale.ordinal()
  .range([  &quot;#aa4748&quot;,&quot;#ff8c00&quot;]);
 
 var xAxis = d3.svg.axis()
  .scale(x0)
  .orient(&quot;bottom&quot;);
 
 var yAxis = d3.svg.axis()
  .scale(y)
  .orient(&quot;left&quot;)
  .tickFormat(d3.format(&quot;.2s&quot;));
    $(&quot;#Res&quot;).empty();
    
 var svg = d3.select(&quot;#Res&quot;).append(&quot;svg&quot;)
  .attr(&quot;width&quot;, width + margin.left + margin.right)
  .attr(&quot;height&quot;, height + margin.top + margin.bottom)
 .append(&quot;g&quot;)
  .attr(&quot;transform&quot;, &quot;translate(&quot; + margin.left + &quot;,&quot; + margin.top + &quot;)&quot;);

 var X_Names = [&apos;A&apos;,&apos;B&apos;,];

 data.forEach(function(d) {
    d.xs = X_Names.map(function(name) { return {name: name, value: +d[name]}; });
 });

 x0.domain(data.map(function(d) { return d.Terms; }));
 x1.domain(X_Names).rangeRoundBands([0, x0.rangeBand()]);
 y.domain([0, d3.max(data, function(d) { return d3.max(d.xs, function(d) { return d.value; }); })]);

 svg.append(&quot;g&quot;)
  .attr(&quot;class&quot;, &quot;x axis&quot;)
  .call(xAxis)
  .attr(&quot;transform&quot;, &quot;translate(0,&quot; + height + &quot;)&quot;)
  .append(&quot;text&quot;)
  .attr(&quot;x&quot;, width+10)
  .attr(&quot;y&quot;, 18)
  .style(&quot;text-anchor&quot;, &quot;end&quot;)
  .text(&quot;Terms&quot;);;

 svg.append(&quot;g&quot;)
  .attr(&quot;class&quot;, &quot;y axis&quot;)
  .call(yAxis)
  .append(&quot;text&quot;)
  .attr(&quot;transform&quot;, &quot;rotate(-90)&quot;)
  .attr(&quot;y&quot;,6)
  .attr(&quot;dy&quot;, &quot;.71em&quot;)
  .style(&quot;text-anchor&quot;, &quot;end&quot;)
  .text(&quot;People&quot;);

 var terms = svg.selectAll(&quot;.terms&quot;)
  .data(data)
  .enter().append(&quot;g&quot;)
  .attr(&quot;class&quot;, &quot;terms&quot;)
  .attr(&quot;transform&quot;, function(d) { return &quot;translate(&quot; + x0(d.Terms) + &quot;,0)&quot;; });

 terms.selectAll(&quot;rect&quot;)
  .data(function(d) { return d.xs; })
  .enter().append(&quot;rect&quot;)
  .attr(&quot;width&quot;, x1.rangeBand())
  .attr(&quot;x&quot;, function(d) { return x1(d.name); })
  .attr(&quot;y&quot;, function(d) { return y(d.value); })
  .attr(&quot;height&quot;, function(d) { return height - y(d.value); })
  .style(&quot;fill&quot;, function(d) { return color(d.name); });

 var legend = svg.selectAll(&quot;.legend&quot;)
  .data(X_Names.slice().reverse())
  .enter().append(&quot;g&quot;)
  .attr(&quot;class&quot;, &quot;legend&quot;)
  .attr(&quot;transform&quot;, function(d, i) { return &quot;translate(0,&quot; + i * 20 + &quot;)&quot;; });

 legend.append(&quot;rect&quot;)
  .attr(&quot;x&quot;, width - 16)
  .attr(&quot;width&quot;, 18)
  .attr(&quot;height&quot;, 18)
  .style(&quot;fill&quot;, color);

 legend.append(&quot;text&quot;)
  .attr(&quot;x&quot;, width+12 )
  .attr(&quot;y&quot;, 9)
  .attr(&quot;dy&quot;, &quot;.35em&quot;)
  .style(&quot;text-anchor&quot;, &quot;end&quot;)
  .text(function(d) { return d; });

};

&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
<div style="line-height: 24.0pt; text-align: justify; text-justify: inter-ideograph;">
<span lang="EN-US" style="font-family: , sans-serif; font-size: 13.5pt;"><br></span></div>
<div style="clear: both;"></div>

