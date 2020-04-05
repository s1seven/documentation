# Notarization Application

<div id="swagger-ui"></div>

<script>
  //https://github.com/swagger-api/swagger-ui/wiki/FAQ
  function HideTopbarPlugin() {
    return {
      components: {
        Topbar: function() { return null }
      }
    }
  }

  SwaggerUIBundle({
      url: "/_api/notarization.json",
      dom_id: '#swagger-ui',
      presets: [
          SwaggerUIBundle.presets.apis,
          SwaggerUIStandalonePreset
      ],
      plugins: [
          SwaggerUIBundle.plugins.DownloadUrl,
          HideTopbarPlugin
      ],
      layout: "StandaloneLayout"
  })
</script>
