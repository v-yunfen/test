## Contexts

| **ProjectTargetFrameworks** | **Framework Version** |

| ASP.NET Core Web Application (.NET Core) - Ind Auth | 1.1 |

| ASP.NET Core Web Application (.NET Framework) - No Auth | 1.1 |

| ASP.NET Core Web Application (.NET Core) - No Auth | 2.0 |

| ASP.NET Core Web Application (.NET Framework) - Ind Auth | 2.0 |

## Walkthrough Steps

1. Run VS as Administrator

2. Create ASP.NET Core Web Application > Web Application (Model-View-Controller)

3. F5 with IIS Express --This should just work
      
4. Open Property Pages

5. Create New Profile to debug with IIS

   a. Hit the new button and name the profile "IIS"
   
   b. Set Launch to IIS
   
   c. Check the "Launch browser" checkbox
   
   d. Add environment variable : ASPNETCORE_ENVIRONMENT and set the value to Development
   
   ![Debug with IIS](_images/ASP.NET Core Web App with IIS/change to IIS.PNG)
   
6. Change Debug dropdown (the play button in the toolbar at the top) to IIS

7. F5
      --This should F5 with IIS now and URL of the form http://localhost/WebApp1 should display in the browser 









