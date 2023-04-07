# NuGet Reformatting Issue Repro

This is a repro for the following issue: https://github.com/dotnet/project-system/issues/8076

## Repro Steps & Context

- Have some kind of multi-line exec command in the project file, e.g.:

```
	<Target Name="NSwag" AfterTargets="Build">
		<Exec Command="
			$(NSwagExe_Net60) openapi2csclient ^
			    /input:Infrastructure/Clients/Something/something.json ^
		            /output:Infrastructure/Clients/Something/SomethingApiClient.generated.cs ^
			    /classname:SomethingApiClient ^
			    /namespace:Something ^
			    /GeneratePrepareRequestAndProcessResponseAsAsyncMethods:True ^
			    /JsonLibrary:SystemTextJson ^
		" />
	</Target>
```

- Update a NuGet package via the VS package management UI.
- Observe, that the exec command string gets reformatted into a single-line representation:

```
<Target Name="NSwag" AfterTargets="Build">
    <Exec Command="&#xD;&#xA;			$(NSwagExe_Net60) openapi2csclient ^&#xD;&#xA;			    /input:Infrastructure/Clients/Something/something.json ^&#xD;&#xA;				/output:Infrastructure/Clients/Something/SomethingApiClient.generated.cs ^&#xD;&#xA;				/classname:SomethingApiClient ^&#xD;&#xA;				/namespace:Something ^&#xD;&#xA;				/GeneratePrepareRequestAndProcessResponseAsAsyncMethods:True ^&#xD;&#xA;				/JsonLibrary:SystemTextJson ^&#xD;&#xA;		" />
</Target>
```
