# TALiveProject
This is the source code I created while working on The Tech Academy Live Project. For the last two weeks of my time at the tech academy, I worked with my peers in a team developing a full scale MVC/MVVM Web Application in C#. Working on a legacy codebase was a great learning oppertunity for fixing bugs, cleaning up code, and adding requested features.

Below are descriptions of the stories I worked on, along with code snippets

Back End Stories: <br>
Created CRUD application for production members. An admin can add or remove production members to a table in the database. The photos on the table are converted to byte format for easy storage and retrieval




Front End Stories: <br>
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

