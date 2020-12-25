---
# Page settings
logo: logo-dark.png
layout: section
title: KeyConnect SDK # Define a title of your page
description: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam sed justo diam. Suspendisse gravida lacinia eros a finibus. Fusce interdum ex nec leo sodales, pharetra scelerisque est dapibus. # Define a description of your page
keywords: # Define keywords for search engines
button: 
    label: Get Started
    url: /documentation
    external_url: false
    style: bordered
    icon: play-circle

section:
    html: 
        <div style="width:80%;margin:0 auto">
        <pre class="prettyprint" style="background:#282840;border-radius:10px"><code class="language-java">
        DefaultApi apiInstance = new DefaultApi(
        <br>
        <span class="u-pl-3">new ApiClient().setBasePath("https://www.keyconnect.app")</span>
        <br>
        );
        <br><br>
        try {
        <br>
        <span class="u-pl-3">ServerStatusResponse result = apiInstance.getServerStatus();
        <br>
        <span class="u-pl-3">System.out.println(result);</span>
        <br>
        } catch (ApiException e) {
        <br>
        <span class="u-pl-3">System.err.println("Exception when calling DefaultApi#getServerStatus");</span>
        <br>
        <span class="u-pl-3">e.printStackTrace();</span>
        <br>
        }
        </pre></code>
        </div>

---
