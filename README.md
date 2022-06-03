# TALiveProject
This is the source code I created while working on The Tech Academy Live Project. For the last two weeks of my time at the tech academy, I worked with my peers in a team developing a full scale MVC/MVVM Web Application in C#. Working on a legacy codebase was a great learning oppertunity for fixing bugs, cleaning up code, and adding requested features.

Below are descriptions of the stories I worked on, along with code snippets

<h1>Back End Stories: </h1><br>
Created CRUD application for production members. An admin can add or remove production members to a table in the database. The photos on the table are converted to byte format for easy storage and retrieval

```
public byte[] createPhotoByte(HttpPostedFileBase postedFile)
        {
            byte[] bytes;
            using (BinaryReader br = new BinaryReader(postedFile.InputStream))
            {
                bytes = br.ReadBytes(postedFile.ContentLength);
            }
            return bytes;
        }

```
This is the photo conversion to a byte so it is able to be stored in the database table

```

public ActionResult Create([Bind(Include = "ProductionMemberId,Name,YearJoined,MainRole,Film,Bio,Photo,CurrentMember,Character,CastYearLeft,DebutYearLeft")] ProductionMember productionMember, HttpPostedFileBase postedFile)
        {
            if (postedFile != null)
            {
                productionMember.Photo = createPhotoByte(postedFile);
                if (ModelState.IsValid)
                {
                    db.ProductionMembers.Add(productionMember);
                    db.SaveChanges();
                    return RedirectToAction("Index");
                }
            }
            else
            {
                if (ModelState.IsValid)
                {
                    db.ProductionMembers.Add(productionMember);
                    db.SaveChanges();
                    return RedirectToAction("Index");
                }
            }
            return View(productionMember);
        }

```
This is the method used to create a new production member, the if else statement is to allow for a null photo.

<h1>Front End Stories: </h1>
On the index page, production members are displayed on cards, organized by the production film they are associated with.

```
@foreach (var group in groupByProduction)
{
    <br />
    <h2 class="">@group.Key</h2>
    <hr />
    <div class="body-content row">
        @foreach (var item in group)
        {
        string text = "";
        if (item.Photo != null)
        {
        text = Convert.ToBase64String(item.Photo);

        <div class="card-deck" style="display: inline-block; width: 18rem;">
            <i class="fa-paperclip:before icon-white"></i>
                <div class="card">
                    <a href="@Url.Action("Details", new { id = item.ProductionMemberId })">
                        <img src="data:image;base64,@text" class="ProductionMembers-Index-Photo" style="height: 12rem;" alt="No available photo">
                    </a>
                    <div class="card-body cms-bg-main-light ProductionMembers-text-card">
                        <h5 class="card-title"><strong><u>@Html.DisplayFor(modelItem => item.Character)</u></strong></h5>

                        <p>@Html.DisplayFor(modelItem => item.Name)</p>
                        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                        <i href="#">@Html.ActionLink(" ", "Delete", new { id = item.ProductionMemberId }, new { @class = "fa fa-edit fa-lg cms-text-secondary" })</i>
                        <i href="#">@Html.ActionLink(" ", "Delete", new { id = item.ProductionMemberId }, new { @class = "fa fa-trash fa-lg cms-text-secondary" })</i>
                    </div>
                </div>
           
        </div>
        }
     } 
    </div><br /><br />
 }

```
This is the code that creates and displays every production member. Utilizes FontAwesome for the edit/delete icons


<h1>Other Skills Learned</h1>

<ul>Working with a group of developers to identify front and back end bugs to the improve usability of an application</ul>
<ul>Improving project flow by communicating about who needs to check out which files for their current story</ul>
<ul>Learning new efficiencies from other developers by observing their workflow and asking questions</ul>
<ul>Practice with team programming/pair programming when one developer runs into a bug they cannot solve</ul>
        
