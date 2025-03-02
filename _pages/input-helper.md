---
title: "CUWALID Input Helper"
layout: single
permalink: /input-helper/
author_profile: true
---

<link rel="stylesheet" href="/assets/css/style.css">

<div id="input-helper">
    <p>Welcome to the CUWALID Input Helper! This tool allows you to easily generate JSON configurations for running the different aspects of CUWALID.</p>

    <div class="input-helper-type-container">
        <label for="jsonType">Select the type of input you would like to create:</label>
        <select id="jsonType">
            <option value="cuwalid">CUWALID</option>
            <option value="dryp">DRYP</option>
            <option value="dryp_settings">DRYP Settings</option>
            <option value="storm">Storm</option>
            <option value="stopet">stoPET</option>
            <option value="hydro_forecast">Hydro Forecast</option>
            <option value="impact_forecast">Impact Forecast</option>
        </select>
    </div>

    <div class="input-helper-load-json">
        <label for="jsonUpload" class="input-helper-json-upload-label">
            Optionally, you can upload a previous input file and modify it from there:
        </label>
        <input type="file" id="jsonUpload" accept=".json">
    </div>

    <div id="formContainer" class="input-helper-nested-section"></div>
    <label for="filename">Output Filename:</label>
    <input type="text" id="filename" placeholder="Filename will auto-fill" />
    <button onclick="exportJSON()">Export JSON</button>

    <h3>JSON Preview</h3>
    <pre class="input-helper-json-output" id="jsonOutput">Loading JSON data...</pre>
</div>


<script src="/assets/js/configurations.js"></script>
<script src="/assets/js/input_helper_script.js"></script>
