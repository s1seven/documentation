# Verification Application

<div id="swagger-ui"></div>

<script>
    SwaggerUIBundle({
         url: "https://demo.verification.en10204.io/api/docs/swagger.json",
        dom_id: '#swagger-ui',
        presets: [
            SwaggerUIBundle.presets.apis,
            SwaggerUIStandalonePreset
        ],
        plugins: [
            SwaggerUIBundle.plugins.DownloadUrl
        ],
        layout: "StandaloneLayout"
    })
</script>
