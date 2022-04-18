---
title: "GG369 - Kawartha Wetlands Mapping"
date: 2020-04-17
categories:
  - WLU-GIS
tags:
  - Wilfrid Laurier
  - QGIS
---
# Kawartha Lakes - Wetland Buffer Mapping

**Project Description** - This post is part of the _WLU-GIS_ collection, containing the GIS projects I completed while getting my undergrad at Wilfrid Laurier University, Ontario, Canada. This project uses GQIS, OpenStreetMaps and OpenGov (Ontario GeoHub) data.

The purpose of this map is to identify all the buildings within the map extent that are within the a set buffer size around wetland features. Kawartha Conservation regulation policies are used as technical reference for determining buffer sizes (Evaluated Wetland = 120 meter, Unevaluated Wetlands = 30 meter). See Process Walkthrough (Below) for more details on map creation. This information could be used to identify areas where Sediment and erosion control measures are required, or where particular environmental polices are relevant. This map is a scaled down, non interactive, version of what most Conservation Authorities Use/provide through their online Conservation Mapping (ESRI). 

## Map Statistics
Buildings - Inside Wetland Buffers = 2,832 <br/>
Buildings - Outside Wetland Buffers = 44,079 <br/>
Evaluated Wetlands = 1,128 <br/>
Unevaluated Wetlands = 2,763 <br/>

<p style="text-align: center;">Kawartha Wetland Map</p>
![GG369 Map 1](/assets/images/gg369/wetlandmap1.jpg)

## Process Walkthrough
- Add XYZ Layer (OpenStreetMap)
- Define Map Extent
     - Create New ShapeFile Layer (Polygon)
     - Edit Feature, Add Polygon Feature, Create Square.
     - Rename "Map Boundary"
- Add Source Layers
    - Ont_Wetlands.shp
    - Ont_Waterbodies.shp
    - Ont_Buildings.shp
    - Reproject from WGS 84 to NAD83 17N (Required for accurate buffering)
- Clip Each Layer to "Map Boundary".
- Separate Evaluated and Unevaluated wetlands
    - Duplicate "Ont_Wetland" Layer
    - Rename "Evaluated Wetland" and "Unevaluated Wetland"
    - Open Attribute table for "Evaluated Wetland", Toggle Editing
    - Filter Features for "Unevaluated", Select Features, Delete Selected Features
    - Repeat for "Unevaluated Layer"
- Create Wetland Buffers
    - Create 120m Buffer for "Evaluated Wetland" 
    - Create 30m Buffer for "Unevaluated Wetland"
    - Find Difference of Evaluated and Unevaluated buffers to remove overlap
    (Plan was to show buildings in 30m and 120m buff separately, Map too crowded, no real benefit, VETO'd)
    - Merge Evaluated Buffer with result of difference Layer, rename "Wetland Buffers"
- Separate Buildings based on buffer
    - Find Difference between "Ont_Buildings" and "Wetland Buffers", Rename Result "Buildings - Outside Buffer"
    - Clip "Ont_Buildings" with "Wetland Buffers", Rename Result "Buildings - Inside Buffer"
- Create Map Layout
    - Self Explanatory...

## Source Layers
- Ontario Wetland Evaluation Systems - Wetlands <br/>
 (https://geohub.lio.gov.on.ca/datasets/mnrf::wetlands/about) 
- Ontario MNRF - Building as Symbol <br/>
 (https://geohub.lio.gov.on.ca/datasets/mnrf::building-as-symbol/about) 
- OpenStreetMaps <br/> 
 (https://www.openstreetmap.org/#map=13/44.3394/-78.7407&layers=Y)
