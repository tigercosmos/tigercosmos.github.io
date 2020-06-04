---
title: 個體導向馬可夫鍊模擬 Agent-Based Markov Chain Simulation
date: 2016-03-19 12:16:00
tags: [程式, 模擬, 機率]
---

馬可夫鏈 (Markov chain) 或稱馬可夫過程 (Markov process)是一種隨機過程，在數學上只要這傳遞矩陣有一些好的性質，就可以證明經由這馬可夫鏈抽樣的分佈會收斂到想要的機率分佈。
<!-- more --> 

這個程式簡單模擬有一群人，分為 A 和 B 兩種狀態，並且一開始兩種狀態人數相同，而每回合 A 中的每個人會有 aRate 機率變 B，B 中的每個人會有 bRate 的機率變 A。如此進行多回合。
(這邊採用 Agent-Based 而不是直接矩陣運算)

效果如下：

![image](https://user-images.githubusercontent.com/18013815/83796060-f9a67480-a6d2-11ea-8cfb-8377172099b6.png)


程式碼 (將程式碼複製存為 `index.html`，並使用瀏覽器打開)

```html
<!DOCTYPE html>
<html>

<head>
    <title>Simulation</title>
    <meta charset="utf-8">
    <style>
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
    </style>
    <script src="https://d3js.org/d3.v3.min.js"></script>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>
</head>

<body>
    <p>Exchange System</p>
    <p>A to B: ( 0 ~ 1 )</p>
    <input type="number" id="aRate" value='0.2' min='0.0' max='1.0'>
    <p>B to A: ( 0 ~ 1 )</p>
    <input type="number" id="bRate" value='0.1' min='0.0' max='1.0'>
    <button>Result</button>
    <div id="Res"></div>

    <script>
        var aRate, bRate;
        $(document).ready(function () {
            $("button").click(function () {
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
            var res = System.runRounds(),
                data = [];
            for (var i = 0; i <= System.NumRounds; i++) {
                data.push({
                    Terms: i,
                    A: res[i].A,
                    B: res[i].B
                });
            }
            showResult(data);
        }

        var System = (function () {
            var People = [];

            var runRounds = function () {
                var result = [];
                initialize();
                result.push({
                    A: System.NumPeople,
                    B: System.NumPeople
                }); // initial
                for (var i = 0; i < System.NumRounds; i++) {
                    result.push(aRound());
                }
                return result;
            };

            var initialize = function () {
                People = [];
                for (var i = 0; i < System.NumPeople; i++) {
                    People.push(new Person(Pss.A));
                    People.push(new Person(Pss.B));
                }
            };

            var aRound = function () {
                People.forEach(function (ps) {
                    ps.change();
                });
                return count();
            };

            var count = function () {
                var Pp = People;
                var data = {
                    A: 0,
                    B: 0
                };
                for (var i in Pp) {
                    if (Pp[i].State == Pss.A) data.A++;
                    else data.B++;
                }
                return data;
            };

            return {
                NumPeople: 10000,
                NumRounds: 30,
                runRounds: runRounds
            };
        })();

        function Person(state) {
            this.State = state;
        }

        Person.prototype.change = function () {
            this.Rate = (this.State == Pss.A) ? aRate : bRate;
            this.State = (Math.random() < this.Rate) ? 3 ^ this.State : this.State;
        }

        function showResult(data) {
            var margin = {
                    top: 20,
                    right: 20,
                    bottom: 30,
                    left: 40
                },
                width = 900 - margin.left - margin.right,
                height = 500 - margin.top - margin.bottom;

            var x0 = d3.scale.ordinal()
                .rangeRoundBands([0, width - 20], .1);

            var x1 = d3.scale.ordinal();

            var y = d3.scale.linear()
                .range([height, 0]);

            var color = d3.scale.ordinal()
                .range(["#aa4748", "#ff8c00"]);

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

            var X_Names = ['A', 'B', ];

            data.forEach(function (d) {
                d.xs = X_Names.map(function (name) {
                    return {
                        name: name,
                        value: +d[name]
                    };
                });
            });

            x0.domain(data.map(function (d) {
                return d.Terms;
            }));
            x1.domain(X_Names).rangeRoundBands([0, x0.rangeBand()]);
            y.domain([0, d3.max(data, function (d) {
                return d3.max(d.xs, function (d) {
                    return d.value;
                });
            })]);

            svg.append("g")
                .attr("class", "x axis")
                .call(xAxis)
                .attr("transform", "translate(0," + height + ")")
                .append("text")
                .attr("x", width + 10)
                .attr("y", 18)
                .style("text-anchor", "end")
                .text("Terms");;

            svg.append("g")
                .attr("class", "y axis")
                .call(yAxis)
                .append("text")
                .attr("transform", "rotate(-90)")
                .attr("y", 6)
                .attr("dy", ".71em")
                .style("text-anchor", "end")
                .text("People");

            var terms = svg.selectAll(".terms")
                .data(data)
                .enter().append("g")
                .attr("class", "terms")
                .attr("transform", function (d) {
                    return "translate(" + x0(d.Terms) + ",0)";
                });

            terms.selectAll("rect")
                .data(function (d) {
                    return d.xs;
                })
                .enter().append("rect")
                .attr("width", x1.rangeBand())
                .attr("x", function (d) {
                    return x1(d.name);
                })
                .attr("y", function (d) {
                    return y(d.value);
                })
                .attr("height", function (d) {
                    return height - y(d.value);
                })
                .style("fill", function (d) {
                    return color(d.name);
                });

            var legend = svg.selectAll(".legend")
                .data(X_Names.slice().reverse())
                .enter().append("g")
                .attr("class", "legend")
                .attr("transform", function (d, i) {
                    return "translate(0," + i * 20 + ")";
                });

            legend.append("rect")
                .attr("x", width - 16)
                .attr("width", 18)
                .attr("height", 18)
                .style("fill", color);

            legend.append("text")
                .attr("x", width + 12)
                .attr("y", 9)
                .attr("dy", ".35em")
                .style("text-anchor", "end")
                .text(function (d) {
                    return d;
                });

        };
    </script>
</body>

</html>
```
