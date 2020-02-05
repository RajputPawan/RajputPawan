---
title: General Git Workflow Saltmigration
permalink: git_general_workflow.html
sidebar: default_sidebar
tags: [docs]
keywords: disk encryption, encryption
last_updated: Feburary 4, 2020
toc: true
folder: docs
---

<html>
<head>
  <!-- Load the JS file -->
  <script src="js/gitgraph.js"></script>
</head>
<body>
  <div id="graph-container"></div>

  <script>
    const graphContainer = document.getElementById("graph-container");

    // Add Options
    // const options = {
    //  orientation: "horizontal"
    // }
    // const gitgraph = GitgraphJS.createGitgraph(graphContainer, options);
    
    const gitgraph = GitgraphJS.createGitgraph(graphContainer);

    // Simulate git commands with Gitgraph API.
    const master = gitgraph.branch("master");
    master.commit("Initial commit").tag("v1.0.0");

    const integration = gitgraph.branch("integration");
    integration.commit("Add Feature");

    const aFeature = gitgraph.branch("feature/[Task-Number]");
    aFeature
      .commit("add saltcheck test")
      .commit("add saltstate")
      .commit("add second saltstate function")
      .commit("fix typo in saltstate");

    integration.merge(aFeature);

    const secondFeature = gitgraph.branch("secondFeature/[Task-Number]");
    secondFeature
      .commit("add saltcheck test")
      .commit("add saltstate");

    integration.merge(secondFeature);
    
    integration.commit("Prepare next release");

    master.merge(integration).tag("v1.0.1");
    
    integration.commit("Next Feature");

    const thirdFeature = gitgraph.branch("thirdFeature/[Task-Number]");
    thirdFeature.commit("add saltcheck test");

    integration.merge(thirdFeature)

    master.merge(integration).tag("v1.0.2");
    
  </script>

</body>
</html>