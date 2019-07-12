# Homework: 3scale Advanced Development

**Made by:** Caio Medeiros Pinto.

## Table of Contents

[TOCM]

[TOC]

## Business Case

You are a consultant assigned to WebRetail Inc., an e-commerce hosting platform. They are developing a new online retail platform branded "CoolStore" through which their partners can provide a catalog and inventory to sell products through the platform.

WebRetail Inc. is adopting a new microservices architecture and wants to make its retail platform APIs available as REST APIs. It has asked you to lead a proof-of-concept (POC) using Red Hat 3scale API Management. The purpose of the POC is to determine the feasibility of using 3scale API Management for managing WebRetail’s APIs, providing a standard portal for its partners to access the APIs, setting up partner tier-based plans, providing standard API documentation, and automating signup for the developers.

## Business Service

WebRetail Inc. has made its CoolStore microservices project available to you:

* Microservices: https://github.com/jbossdemocentral/coolstore-microservice

* Additional collateral: https://github.com/gpe-mw-training/3scale_development_labs/tree/master/CoolStore

## Environment Details

Two APIs was created in 3scale platform to manage both microservices that WebRetail has. The first one is Inventory Service, that has 2 Applications plans: Inventory Service Basic and Inventory Service Premium. And the another one is Catalog Service and has the Application plans: Catalog Service Basic and Catalog Service Premium.

The default API definition was deleted to be sure that it won't be available througt the Developer Portal.

By configuration reasons, was created applications with both APIs basic plans linked to the default developer organization.

### 3Scale Web Portals

|Portal|URL|User|Password|
|---|---|----|--------|
|Admin|https://user4-admin.apps-08b3.generic.opentlc.com|user4|r3dh4t1!|
|Developer|https://user4.apps-08b3.generic.opentlc.com|-----|-----|

### Inventory Service API URL

|URL|Environment|
|---|-----------|
|https://inventory-service-user4-apicast-staging.apps-08b3.generic.opentlc.com|Staging|
|https://inventory-service-user4-apicast-production.apps-08b3.generic.opentlc.com|Production|

### Catalog Service API URL

|URL|Environment|
|---|-----------|
|https://catalog-service-user4-apicast-staging.apps-08b3.generic.opentlc.com|Staging|
|https://catalog-service-user4-apicast-production.apps-08b3.generic.opentlc.com:|Production|

## CURL Commands

### CURL Inventory API

**Get inventory item**:

```bash
$ curl "https://inventory-service-user4-apicast-production.apps-08b3.generic.opentlc.com:443/inventory/329299?user_key=9a50126b0ebcadc99ad408b2f2e55aa5" -k
{
	"itemId": "329299",
	"location": "Raleigh",
	"quantity": 736,
	"link": "http://maps.google.com/?q=Raleigh"
}
```

### CURL Catalog API

**Get all products**:

```bash
$ curl "https://catalog-service-user4-apicast-production.apps-08b3.generic.opentlc.com:443/products?user_key=f4c5d1c33e828fb6007ef6b234e77ee6" -k
{
  "version" : "v1",
  "data" : [ {
    "itemId" : "329299",
    "name" : "Red Fedora",
    "desc" : "Official Red Hat Fedora",
    "price" : 34.99
  }, {
    "itemId" : "329199",
    "name" : "Forge Laptop Sticker",
    "desc" : "JBoss Community Forge Project Sticker",
    "price" : 8.5
  }, {
    "itemId" : "165613",
    "name" : "Solid Performance Polo",
    "desc" : "Moisture-wicking, antimicrobial 100% polyester design wicks for life of garment. No-curl, rib-knit collar; special collar band maintains crisp fold; three-button placket with dyed-to-match buttons; hemmed sleeves; even bottom with side vents; Import. Embroidery. Red Pepper.",
    "price" : 17.8
  }, {
    "itemId" : "165614",
    "name" : "Ogio Caliber Polo",
    "desc" : "Moisture-wicking 100% polyester. Rib-knit collar and cuffs; Ogio jacquard tape inside neck; bar-tacked three-button placket with Ogio dyed-to-match buttons; side vents; tagless; Ogio badge on left sleeve. Import. Embroidery. Black.",
    "price" : 28.75
  }, {
    "itemId" : "165954",
    "name" : "16 oz. Vortex Tumbler",
    "desc" : "Double-wall insulated, BPA-free, acrylic cup. Push-on lid with thumb-slide closure; for hot and cold beverages. Holds 16 oz. Hand wash only. Imprint. Clear.",
    "price" : 6.0
  }, {
    "itemId" : "444434",
    "name" : "Pebble Smart Watch",
    "desc" : "Smart glasses and smart watches are perhaps two of the most exciting developments in recent years. ",
    "price" : 24.0
  }, {
    "itemId" : "444435",
    "name" : "Oculus Rift",
    "desc" : "The world of gaming has also undergone some very unique and compelling tech advances in recent years. Virtual reality, the concept of complete immersion into a digital universe through a special headset, has been the white whale of gaming and digital technology ever since Nintendo marketed its Virtual Boy gaming system in 1995.",
    "price" : 106.0
  }, {
    "itemId" : "444436",
    "name" : "Lytro Camera",
    "desc" : "Consumers who want to up their photography game are looking at newfangled cameras like the Lytro Field camera, designed to take photos with infinite focus, so you can decide later exactly where you want the focus of each image to be.",
    "price" : 44.3
  } ]
}
```

**Get product**:

```bash
$ curl "https://catalog-service-user4-apicast-production.apps-08b3.generic.opentlc.com:443/product/329299?user_key=f4c5d1c33e828fb6007ef6b234e77ee6" -k
{
  "version" : "v1",
  "data" : {
    "itemId" : "329299",
    "name" : "Red Fedora",
    "desc" : "Official Red Hat Fedora",
    "price" : 34.99
  }
}
```

## Developer Portal Customizations

### Page Documentation

Changed the word **Echo API** to **services**.

### Page Homepage

The chages were the following:

1. Lines from 119 to 182 were deleted.
2. Snippet added at the line 119 (Near to `{% endif %}`), the snipet is:

   ```liquid
   <section class="plan">
    {% include 'multi_app_signup_form' %}
   </section>
   ```

3. The HTML h1 tag in the line 5 was replaced by: `<h1>WebRetail API Catalog</h1>`.
4. The text in the line 19 was replaced by: This is your API key that should be kept secret. Use it to authenticate and report the calls you make to the services.
5. The lines from 91 to 117 were replaced by the follow:

   ```html
   <section class="sell">
    <div class="container">
      <div class="row">
        <div class="col-md-4">
          <h3>Select the service plans</h3>
          <p>
          <i class="fa fa-sign-in fa-3x pull-left"></i>
          Go below and select the plans of services that you want.
          </p>
        </div>
        <div class="col-md-4">
          <h3>Register</h3>
          <p>
          <i class="fa fa-key fa-3x pull-left"></i>
          Register to the developer portal to use the selected services.
          </p>
        </div>
       <div class="col-md-4">
        <h3>Create your app</h3>
         <p>
         <i class="fa fa-code fa-3x pull-left"></i>
         Start coding and create awesome applications with the services.
         </p>
        </div>
       </div>
      </div>
    </section>
   ```

6. Lines from 123 to the end were deleted.

Finally the page was saved and published.

### File default.css

Is placed in `Root/css`, was made a single change that is:

```css
[...]
/* Home page */
.page-header {
  display: block;
  background-position: center center;
  background-image: url('/images/logo.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  margin: 0 0 0 0;
  padding: 0 0 0 0;
  border-bottom: none;
}
[...]
```

This change was made to use another image for the homepage banner.
Finally the page was saved and published.

### Partial multi_app_signup_form

Created using the following content:

```liquid
<form id="process-form" action="{{ urls.signup }}" method="get">
  <div class="container">
    <h1>Pick your plan</h1>
    <br/>
    {% for service in provider.services %} 
    <h2> {{ service.name }} </h2>
    <div class="row">
      {% for plan in service.application_plans%}
      <div class="col-md-4">
        <article class="panel panel-default">
          <div class="panel-heading">
            <strong>{{ plan.name }}</strong>
          </div>
          <div class="panel-body">
            <div class="row">
              {% if plan.features == present %}
              <div class="col-md-6">
                <h5>Features</h5>
                <ul class="features list-unstyled">
                  {% for feature in plan.features %}
                  <li>
                    <i class="fa fa-check"></i> {{ feature.name }}
                  </li>
                  {% endfor %}
                </ul>
              </div>
              {% endif %}
              <div class="col-md-6">
                <h5>Limits</h5>
                <ul class="limits list-unstyled">
                  {% if plan.usage_limits == present %} {% for limit in plan.usage_limits %}
                  <li>
                    <i class="fa fa-signal"></i> {{ limit.metric.name }} &ndash; {{ limit.value }} {{ limit.metric.unit }}s per {{ limit.period }}
                  </li>
                  {% endfor %} {% else %}
                  <li>
                    <i class="fa fa-signal"></i> No limits
                  </li>
                  {% endif %}
                </ul>
              </div>
            </div>
          </div>
          <div class="panel-footer">
            <div class="row">
              <div class="col-md-12">
                <div class="row">
                  <div class="col-md-12">
                    <input type="checkbox" name="plan_ids[]" value="{{ plan.id }}">Signup to {{ plan.name }}</input>
                    <input type="hidden" name="plan_ids[]" value="{{ service.service_plans.first.id }}"></input>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </article>
      </div>              
      {% endfor %}
    </div>
    {% endfor %}
    <div class="container text-center">
      <div class="alert alert-info" role="alert">
        The <strong>Premium plans</strong> need approval.
      </div>
      <input id="raptorize" type="hidden" />
      <button type="submit" class="btn btn-primary btn-lg">Signup</a>
    </div>
  </div>
</form>

<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.3/jquery.min.js"></script>
<script>!window.jQuery && document.write('<script src="jquery-1.4.3.min.js"><\/script>')</script>
<script src="jquery.raptorize.1.0.js"></script>

<script type="text/javascript">
  $(window).load(function() {
    $('#raptorize').raptorize();
    $('#process-form').submit(function(event) {
      var form = this;
      event.preventDefault();
   	  $('#raptorize').trigger('click');
      setTimeout( function () { 
        form.submit();
      }, 3000);
    });
  });
</script>
```

### Partial shared/swagger_ui

Was completely changed by the following content:

```liquid
<div class='apidocs-param-tips apidocs-signin-message' style='display:none;'>
    <p><a href='#'>Sign in</a> to your account for quick access to useful values.</p>
</div>

{% for api in provider.api_specs %}

<div class="swagger-section">
    <div id="message-bar-{{ api.system_name }}" class="swagger-ui-wrap">&nbsp;</div>
    <div id="swagger-ui-container-{{ api.system_name }}" class="swagger-ui-wrap"></div>
</div>

{% endfor %}

<script type = "text/javascript" >
  $(function() {
    {% for api in provider.api_specs %}
    
    window.anotherSwaggerUi = new SwaggerUi({
      url: "{{ api.url }}",
      dom_id: "swagger-ui-container-{{ api.system_name }}",
      supportedSubmitMethods: ['get', 'post', 'put', 'delete', 'patch'],
      onFailure: function(data) {
        console.log("Unable to Load Sentiment-SwaggerUI");
      },
      docExpansion: "list",
      transport: function(httpClient, obj) {
        console.log("[swagger-ui]>>> custom transport.");
        return ApiDocsProxy.execute(httpClient, obj);
      }
    });
    window.anotherSwaggerUi.load();

    {% endfor %}
  }); 
</script>
```

### Raptorize Jquery plugin

To enable that go to the rapitorize page and download the kit, and create each file in the `.Root` path of Developer Portal. Is important that the file name was declared in the **Path** input.
