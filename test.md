## Walkthrough Steps

### Create project with empty template

1. File > New Project > ASP.NET Core Web Application. Give a name, eg: SimpleAppWithEmpty1

    ![Project template](_images/20_SimpleWebAppWithEmptyTemplate_MVC/proj_template.PNG)

2. Choose either one of these two template - "ASP.NET Core Web Application on .NET Core" or "ASP.NET Core Web Application on .NET Framework"

    ![Project template type](_images/20_SimpleWebAppWithEmptyTemplate_MVC/proj_template_type.PNG)

3. Select "Empty" template in the New ASP.NET Core dialog and hit OK

4. Wait for package restore to complete, verify package restore completes successfully without any error

    - View Output window > package Manager pane in Output window will show restore status

    - Wait till package restore completes

    ![Verify message in Output](_images/20_SimpleWebAppWithEmptyTemplate_MVC/verify_output_info.PNG)

### Build and run

1. Open Startup.cs, build the project. Verify no errors or warnings in the output window and in the error list

    ![Build and verify error list](_images/20_SimpleWebAppWithEmptyTemplate_MVC/build_verify_errorlist.PNG)

2. Run the project and verify you get "Hello world!" in the browser

### Add html page and browse to it

1. Add the following line in Startup.cs in the Configure method,the place is just showed as below.

    ![Add code in Configure method](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_usefileserver_in_configure.PNG)

    ```
    app.UseFileServer();
    ```

    **NOTE:** For ASP.NET Core Web Application on **.NET Framework** template (This steps only for .NET Framework 2.0 template):

    - Make sure Package source to 'All' to find the latest version
    
    You may need to add "Microsoft.AspNetCore.StaticFiles" package using NuGet Package Manager dialog.

    Or edit .csproj file , add following code:
    
    > <PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="2.0.**_latest_**" />

2. Add new "index.html" file to wwwroot folder, add the content below

    ```
    <div>
		<p>Hello from HTML page</p>
	</div>
    ```
    ![Add content to index.html file](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_content_to_index.PNG)

### Add solution to source control

1. Right-click solution > Add Solution to Source Control -- this should automatically check-in the solution into Git SCC

### Wire up MVC, add MVC controller with a View and browse to /Home

1. Update the ConfigureServices and Configure method in Startup.cs

    a. Add MVC service to ConfigureServices method
    
    > services.AddMvc();

    ![Add MVC service to ConfigureServices method](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_service_to_configureservices.PNG)

    **NOTE:** For ASP.NET Core Web Application on **.NET Framework** template (This steps only for .NET Framework 2.0 template):

    You may need to add "Microsoft.AspNetCore.Mvc" package using NuGet Package Manager dialog.

    Or edit .csproj file, add following code:			

    > <PackageReference Include="Microsoft.AspNetCore.Mvc" Version="2.0.**_latest_**" />

    b. Configure default MVC route, comment out the highlight part and replace it with the following codes 
    
    ```
    app.UseMvc(routes => 
	{
	    routes.MapRoute(
			name: "default",
			template: "{controller=Home{action=Index/{id?}");
    });
    ```
    
    ![Add MVC route to Configure method](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_mvcroute_to_configure.PNG)

2. Add a HomeController using scaffolding 

    a. Add Controllers folder to root of the project

    b. Right-click Controllers folder > Add Controller > "MVC Controller-Empty" and provide the name as "HomeController"
    ![Add HomeController](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_homecontroller.PNG)

    c. Add a View page for the Index action of HomeController

    d. Add a Views folder to root of the project. Add Home folder under Views. 

    e. Right-click Home folder > Add View

    f. In the "Add View" dialog, uncheck "Use layout page" and click Add

      ![Add View page for Index action](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_view.PNG)

    g. Rename the file to Index.cshtml

3. Replace the contents of the file with the following code and save

    ```
    <html xmlns="http://www.w3.org/1999/xhtml">
		<head>
		    <title></title>
		</head>
		<body>
		  <div>
			<p>Hello from MVC View Page</p>
			<p>@ViewData["message"]</p>
		  </div>
		</body>
	</html>
    ```

4. Pass in a message from the HomeController.cs using ViewData

    > ViewData["message"] = "Message from the controller";

    ![Get message using ViewData](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_viewdata_homecontroller.PNG)

### Build and run, verify "Fast Refresh"

1. Open Startup.cs, build the project. Verify no errors or warnings In the output window and in the error list

    ![Verify error list](_images/20_SimpleWebAppWithEmptyTemplate_MVC/fastrefresh_verify_errorlist.PNG)

2. Run the project (Ctrl-F5) and verify you get "Hello from Html page" in the browser (from the HTML page)

3. Navigate to **/Home** in the browser and verify you get "Hello from MVC View Page" and "Message from the controller"

    ![Verify the message in browser before message change](_images/20_SimpleWebAppWithEmptyTemplate_MVC/fast_refresh_before.PNG)

4. Go to Index.cshtml and change "View Page" to "View Page 1", and save the file

5. Go to HomeController.cs and change "Message from the controller" to "Message 1 from the controller"

6. Switch back to the browser (use alt-tab, do not hit Ctrl-F5 again), and hit the Refresh button on the browser, verify browser gets immediately reloaded with the new content

    ![Verify the message in browser after it changed in VS](_images/20_SimpleWebAppWithEmptyTemplate_MVC/fast_refresh_after.PNG)

### Publish to Azure - Create a new web app on Azure and publish this project to Azure

1. Right-click project > Publish, choose Azure App Service > Create New

2. Create New Web app in existing or new Resource Group / App Service Plan, no database needed for this project

    ![Publish the project](_images/20_SimpleWebAppWithEmptyTemplate_MVC/proj_publish_new.PNG)

3. Click Settings link in Publish pane, navigate to Connection tab > Validate Connection

    ![Verify the validate connection](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_validate_connection.PNG)
    
4. Navigate to Settings tab, pick the default options, select "Remove additional files at destination" and click Save

    ![Check the checkbox in Setting tab](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_settings.PNG)

5. Click Preview link in Publish pane, click Start Preview

    ![Preview](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_preview.PNG)

6. Publish to Azure, verify index.html page loads properly on published Azure site. Navigate to /Home and verify MVC view loads fine too

    ![Verify index.html page loads properly after publish](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_default.PNG)

    ![Navigate to /Home, verify the page loads fine](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_home.png)

### Add some basic bootstrap styling to index.html

1. Right-click project > Add > New Item... >  bower.json

    ![Add bower.json file](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_bower_file.PNG)

2. Type "bootstrap":"" to bower.json, use intellisense to pick the latest stable version of the package.(Do save the modification!)

    ![Use intellisense to pick the version of package](_images/20_SimpleWebAppWithEmptyTemplate_MVC/intellisense_bower.PNG)

3. Open index.html, find bootstrap.css under wwwroot\lib\bootstrap\dist folder in Solution Explorer, drag-drop the file to '< head >' section of index.html

    ![Add bootstrap.css to index.html file](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_css_to_index.PNG)

4. Similarly, add jquery.js and bootstrap.js to <body> section

    ![Add bootstrap.css to index.html file](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_js_to_index.PNG)

5. Change the code in body to the following

    ```
    <div class="jumbotron">
        <p>Simple HTML page using Bootstrap</p>
        <div class="col-sm-6 subHeading">
            <h4>Sub heading 1</h4>
        </div>
        <div class="col-sm-6 subHeading">
            <h4>Sub heading 2</h4>
        </div>
    </div>
    ```

    ![Change code in body to index.html file](_images/20_SimpleWebAppWithEmptyTemplate_MVC/add_js_to_index.PNG)

6. Remove class="jumbotron" from above and type it in again. Verify you get Bootstrap intellisense

    ![Verify the intellisense in index.html file](_images/20_SimpleWebAppWithEmptyTemplate_MVC/bootstrap_intellisense_index.PNG)

7. Ctrl-F5, verify bootstrap-styled page shows up in browser

    ![Verify bootstrap-styled page shows up in browser](_images/20_SimpleWebAppWithEmptyTemplate_MVC/bootstrap_style.PNG)

### Publish to Azure again

1. Click Preview link in Publish pane > Preview changes

2. Publish to Azure again, verify bootstrap-styled page shows up in the published Azure site, and you can still navigate to /Home

    ![Verify bootstrap-styled shows up in Azure site](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_changes_default.png)

    ![Navigate to Home and verify the page loads in Azure site](_images/20_SimpleWebAppWithEmptyTemplate_MVC/publish_change_home.png)
