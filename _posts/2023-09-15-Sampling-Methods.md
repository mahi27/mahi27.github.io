---
layout: post
title: Sampling Methods - All You Need To Know!
author: sal
categories: [ Sampling, Python ]
featured: false
hidden: false
ml101: true
image: assets/images/randomsample.jpg
---

<style>

.node {
  cursor: pointer;
}

.node circle {
  fill: #fff;
  stroke: steelblue;
  stroke-width: 1.5px;
}

.node text {
  font: 10px sans-serif;
}

.link {
  fill: none;
  stroke: #ccc;
  stroke-width: 1.5px;
}

</style>
    
<link href="https://afeld.github.io/emoji-css/emoji.css" rel="stylesheet">
<h2><strong>Introduction</strong></h2>
<p>Sampling is the process of creating a representative set of population. It’s almost impossible to analyze/survey a population to arrive at the results. Sampling allows for large-scale research at a realistic cost and time. There are various sampling techniques to choose from depending on the usecase, we will cover the most commonly used ones in this article.</p>

<div id='d3div'></div>

<h2><strong>Probability Sampling</strong></h2>
<p>Probability sampling is a technique in which every element in the population has an equal chance of being chosen. Since such sample would be unbiased and random, we can estimate the sampling error and the degree of confidence. This technique is best suitable for descriptive studies with large and diverse population.</p>

<strong>Simple Random Sampling</strong>
<p>This is a basic sampling method, where a subset is randomly selected from the population. It is popular for its simplicity and lack of bias.</p>

```
#Simple Random Sampling
from sklearn.datasets import load_iris
import pandas as pd
import numpy as np
#load iris dataset
iris = load_iris()
df = pd.DataFrame(data=np.c_[iris['data'], iris['target']],
        columns= iris['feature_names'] + ['target']).astype({'target': int}) \
       .assign(species=lambda x: x['target'].map(dict(enumerate(iris['target_names']))))
#sample 100 rows from iris dataset
simple_random = df.sample(n=50)
```

{% include simple_random.html %}

<strong>Systematic Sampling</strong>
<p>In this method, members of the sample are selected from population in a systematic way - at a fixed sampling interval from a random starting point. Compared to simple random sampling, this method has higher degree of control and low chance of data contanimation. Size of population is needed beforehand for this method to work well.</p>

```
# systematic sampling function
# 0 as starting point
def systematic_sampling(df, step):
    rows = np.arange(0, len(df), step=step)
    systematic_sample = df.iloc[rows]
    return systematic_sample

#sample every 3rd row
systematic_sample = systematic_sampling(df,3)
```

{% include systematic_sample.html %}

<strong>Stratified Sampling</strong>
<p>This method involves division of population into subsets or strata. Proportionate sampling takes each strata in the sample proportionate to the population size while disproportionate sampling, certain strata will oversample or undersample based on research question.</p>

```
#proprotionate stratified sampling
from sklearn.model_selection import train_test_split
#sample 30% of the data
stratified_sample,_ = train_test_split(df, test_size=0.7, stratify=df["species"])
```

{% include stratified_sample.html %}

<strong>Cluster Sampling</strong>
<p>In this method, population is divided into clusters and then some of the clusters are randomly selected as the sample. There are variations to this method such as single-stage, double-stage and multi-stage each adding randomness with the stages. This method is used when the population is too spread out. This method can result in a high sampling error if the clusters aren't representative of the population.</p>

```
#single stage cluster sampling
import random
def cluster_sampling(df,clusters,n):
    df['cluster'] = np.random.randint(0,clusters+1,size = len(df))
    rows = random.sample(range(0,clusters+1),n+1)
    cluster_sample = df[df.cluster.isin(rows)]
    return cluster_sample

cluster_sample = cluster_sampling(df,10,3)
```

{% include cluster_sample.html %}

<h2><strong>Nonprobability Sampling</strong></h2>
<p>Nonprobability sampling is a technique in which elements have unequal chance of being chosen. This technique is best suited for exploratory studies on small and specific population. It is not intended to draw any statistical conclusions about the population.</p>

<strong>Convenience Sampling</strong>
<p>In this techqniue, sampling is done based on availability and relative ease of access. Researchers usually use this method to gather feedback on critical issues/products. Online surveys, market research on university campus, interviewing people at a mall are examples of this method.</p>

<strong>Judgemental Sampling</strong>
<p>In this method, sampling is done based on researcher's judgement or expertise. This is often used when certain participants/elements of the population are more relevant to the research objective. Expert panels, celebrity interviews, clinical trials are examples of this method.</p>


<strong>Quota Sampling</strong>
<p>This method is similar to stratified sampling, where researcher idenities subsets of population and then selects memebers non-randomly based on pre-specified quota. This is often used in when researcher wants to ensure that sample is representative of population based on certain attributes like geographic region, age, gender or income.</p>


<strong>Snowball Sampling</strong>
<p>This technique involves selecting a small group of people and relying on their referrals to identify additional participants for the sample. It can result in a biased sample, and researchers should be wary that it might not be representative of the population. This method is useful when population is difficult to reach or hidden. </p>

<h2><strong>Other Sampling Methods</strong></h2>
<p>Most ML algorithms are designed to work on balanced datasets for classification. When the data is imbalanced, the minority class is often ignored, and the minority class ends up with a high misclassification rate. This is because most ML algorithms rely on the class distribution to gauge the likelihood and make predictions.</p>
<p>Here’s where data sampling will help by transforming the imbalanced dataset to a balanced one. This allows for the algorithms to train on the modified dataset without additional data preparation. Random Oversampling, Random Undersampling, SMOTE, ADASYN, Tomek Links are some of the popular sampling methods for imbalanced datasets.


<p>If you found my work useful, please cite it as:</p>
<pre>
{
  author        = {Tammineedi, Mahitha},
  title         = {Sampling Methods - All you need to know},
  howpublished  = {\url{https://mahi27.github.io/}},
  year          = {2023},
  note          = {Accessed: 2023-09-15},
  url           = {https://mahi27.github.io/}
}

M. Tammineedi, Sampling Methods - All you need to know , https://mahi27.github.io/, 2023, Accessed: Sep 15 2023.
 
</pre>


<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.17/d3.min.js"></script>

<script>
var treeData = [
    {
      "name": "Sampling",
      "parent": "null",
      "value": 10,
      "type": "black",
      "level": "black",
      "url": "www.google.com",
      "children": [
        {
          "name": "Probability",
          "parent": "Sampling Techniques",
          "value": 10,
          "type": "black",
          "level": "black",
          "url": "www.google.com",
          "children": [
            {
                "name": "Simple Random Sampling",
                "parent": "Probability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com"
              },
              {
                "name": "Systematic Sampling",
                "parent": "Probability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com"
              },
              {
                "name": "Stratified Sampling",
                "parent": "Probability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com",
                "children": [
                    {
                        "name": "Proportionate Sampling",
                        "parent": "Stratified Sampling",
                        "value": 10,
                        "type": "black",
                        "level": "black",
                        "url": "www.google.com"
                    },
                    {
                        "name": "Disproportionate Sampling",
                        "parent": "Stratified Sampling",
                        "value": 10,
                        "type": "black",
                        "level": "black",
                        "url": "www.google.com"
                    }
                ]
              },
              {
                "name": "Cluster Sampling",
                "parent": "Probability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com"
              }
          ]
        },
        {
          "name": "Nonprobability",
          "parent": "Sampling Techniques",
          "value": 10,
          "type": "black",
          "level": "black",
          "url": "www.google.com",
          "children": [
            {
              "name": "Convenience Sampling",
              "parent": "Nonprobability",
              "value": 10,
              "type": "black",
              "level": "black",
              "url": "www.google.com"
            },
            {
                "name": "Judgemental Sampling",
                "parent": "Nonprobability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com"
            },
            {
                "name": "Quota Sampling",
                "parent": "Nonprobability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com"
            },
            {
                "name": "Snowball Sampling",
                "parent": "Nonprobability",
                "value": 10,
                "type": "black",
                "level": "black",
                "url": "www.google.com"
            }
          ]
        }
      ]
    }
  ];

// ************** Generate the tree diagram	 *****************
var margin = {top: 20, right: 120, bottom: 20, left: 120},
	width = 960 - margin.right - margin.left,
	height = 500 - margin.top - margin.bottom;
	
var i = 0;
var tree = d3.layout.tree()
	.size([height, width]);
var diagonal = d3.svg.diagonal()
	.projection(function(d) { return [d.y, d.x]; });
var svg = d3.select("#d3div").append("svg")
	.attr("width", width + margin.right + margin.left)
	.attr("height", height + margin.top + margin.bottom)
  .append("g")
	.attr("transform", "translate(" + margin.left + "," + margin.top + ")");
root = treeData[0];
update(root);
function update(source) {
  // Compute the new tree layout.
  var nodes = tree.nodes(root).reverse(),
	  links = tree.links(nodes);
  // Normalize for fixed-depth.
  nodes.forEach(function(d) { d.y = d.depth * 180; });
  // Declare the nodes…
  var node = svg.selectAll("g.node")
	  .data(nodes, function(d) { return d.id || (d.id = ++i); });
  // Enter the nodes.
  var nodeEnter = node.enter().append("g")
	  .attr("class", "node")
	  .attr("transform", function(d) { 
		  return "translate(" + d.y + "," + d.x + ")"; });
  nodeEnter.append("circle")
	  .attr("r", function(d) { return d.value; })
	  .style("stroke", function(d) { return d.type; })
	  .style("fill", function(d) { return d.level; });
  
  nodeEnter.append("a")
    .attr("xlink:href", function(d) { return d.url; })
    .append("text")
    .attr("x", function(d) { 
		  return d.children || d._children ? 
		  (d.value + 4) * -1 : d.value + 4 })
	  .attr("dy", ".35em")
	  .attr("text-anchor", function(d) { 
		  return d.children || d._children ? "end" : "start"; })
	  .text(function(d) { return d.name; })
    .attr("xlink:href", function(d) { return d.url; })
	  .style("fill-opacity", 1);
  // Declare the links…
  var link = svg.selectAll("path.link")
	  .data(links, function(d) { return d.target.id; });
  // Enter the links.
  link.enter().insert("path", "g")
	  .attr("class", "link")
  	  .style("stroke", function(d) { return d.target.level; })
	  .attr("d", diagonal);
}
</script>
