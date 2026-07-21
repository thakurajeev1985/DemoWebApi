**For Api Versioning**

**Step 1. Add refferences from NuGet package manager**

        Asp.Versioning.Mvc, Asp.Versioning.Mvc.ApiExplorer



**Step 2. Add at Controller lavel**

        [ApiVersion("1.0")]
        [Route("api/v{version:apiVersion}/[controller]")]

        [ApiVersion("2.0")]
        [Route("api/v{version:apiVersion}/[controller]")]
        
        
**Step 3. Add services to the container. in program.cs before builder.Services.AddControllers();**

       builder.Services.AddApiVersioning(options =>
        {
            options.DefaultApiVersion = new ApiVersion(1, 0);
            options.AssumeDefaultVersionWhenUnspecified = true;
            options.ReportApiVersions = true;
            options.ApiVersionReader = ApiVersionReader.Combine(
            new UrlSegmentApiVersionReader(),
            new HeaderApiVersionReader("X-Api-Version")
            );
        })
        .AddApiExplorer(options =>
        {
            options.GroupNameFormat = "'v'VVV";
            options.SubstituteApiVersionInUrl = true;
        }); 
