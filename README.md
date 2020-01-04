# Blazor Scaffolded Identity
Scaffolded Blazor App with fixed Logout

>IF USING THIS REPO DELETE TEST USER - user@user.com 


1. dotnet new blazorserver --auth Individual
2. create new user for testing ( user@user.com / Pass12345! )
3. login and logout and it's working
4. install if not already ( dotnet tool install --global dotnet-aspnet-codegenerator --version 3.1.0 )
5. add package to project | dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 3.1.0
6. add package to project | dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 3.1.0
7. do a scaffold | dotnet aspnet-codegenerator identity -dc BlazorScaffoldedIdentity.Data.ApplicationDbContext --force
8. logout from blazor - not working
9. using instructions from ScaffoldingReadMe.txt
10. logout from blazor - not working

#### NOTE:
1. if user go to https://localhost:5001/Identity/Account/Manage ,  then from _MangeNav.cshtml can succesfuly LogOut from app.


#### WORKAROUND NUM 1:
    Add [IgnoreAntiforgeryToken] in "LogOut.cshtml.cs" file

#### WORKAROUND NUM 2:
- delete files in areas/pages/account "LogOut.cshtml" and "LogOut.cshtml.cs", and create new file that is like the one before scaffold ( "LogOut.cshtml" )

            @page
            @using Microsoft.AspNetCore.Identity
            @attribute [IgnoreAntiforgeryToken]
            @inject SignInManager<IdentityUser> SignInManager
            @functions {
                public async Task<IActionResult> OnPost()
                {
                    if (SignInManager.IsSignedIn(User)){await SignInManager.SignOutAsync();}
                    return Redirect("~/");
                }
            }
