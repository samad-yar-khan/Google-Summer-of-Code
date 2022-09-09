<div align="center">
       <h1> 
        <p>
           <a href="https://github.com/RocketChat/Apps.Github22">GitHub App </a> for <a href="https://rocket.chat/">Rocket.Chat</a>
        </p>
      </h1>
    <a href="https://summerofcode.withgoogle.com/projects/#6521788818784256"><img src="https://i.imgur.com/pgkUceb.png" width="650" alt="google-summer-of-code"></a>
    <br>
</div>

<p align="center">
    <code> 
        <a href="#-project-abstract">Project Abstract</a>&nbsp;&nbsp;&nbsp;
        <a href="#-deliverables">Deliverables</a>&nbsp;&nbsp;&nbsp;
        <a href="#-demo">Demo</a>&nbsp;&nbsp;&nbsp;
        <a href="#-contributions">Contributions</a>&nbsp;&nbsp;&nbsp;
        <a href="#-blog">Blog</a>&nbsp;&nbsp;&nbsp;
        <a href="#-mentors">Mentors</a>&nbsp;&nbsp;&nbsp;
        <a href="#-links">Links</a>
    </code>
</p>

During Google Summer of Code 2022 I worked on the GitHub App for Rocket.Chat. This a GitHub itegration for RocketChat which enables developers to use various GitHub features inside RocketChat channels.

I intend to maintain this repository as a final report summary of my GSoC work and a quick guide for all future GSoC aspirants.

## ⭐ Project Abstract

The GitHub Rocket.Chat App provides a seamless integration between GitHub and Rocket.Chat and improves collaboration between developers. The application allows users to search and share Issues and Pull Request, Subscribe to Repository Events, Create New Issues, Review and Merge Pull Requests, Assign issues to users and do much more right from Rocket.Chat.

## 🚢 Deliverables

The following were the deliverables of this project:

- Minimal  Slash Command Interface : Adding slash command to trigger the application to fetch details and data of any GitHub repository.
- Event Subscriptions : Allow users to subscribe to single/multiple events of a repository using GitHub Webhooks and get notified of changes to a repository.
- Extensive Queries : Enable Querying of issues/pull request/repository based on labels, author etc. 
- New Issues : Ability to raise issues in a repository right from Rocket.Chat using an interactive modal interface.
- Issue-Assignees : Ability to make an Issue-Assignee list for a repository in a channel to assign and track issues allotted to team members.
- Code Changes : Enable users to view the code changes done by a pull request using a built-in code editor and merge the pull request.
- Build Interactive UI : Unlock the true potential of the UiKit and add an interactive user interface for each of the added features of the application, eliminating the need to type long slash commands for more complex tasks.

Extra Features which were suggested by mentors throughout the Google Summer of Code period:

- Adding Scalable Authentication Mechanism : Deleting the OAuth tokens from the Apps Local Storage after a period of time using [Scheduler API](https://developer.rocket.chat/apps-engine/adding-features/scheduler-api).
- GitHub Search and Share : 
  - Extensive Queries feature was extended to GitHub Search, where users could search issues and pull requests on GitHub by adding multiple filters inside an interactive modal.
  - Multiple Search Results can be shared in the channel along with a personalized message.
- Issue Templates : The New Issues feature was extened to fetch repository issue templates from GitHub, any of which could be selected to open a new issue from Rocket.Chat. 

**All of the above deliverables were completed within the GSoC period. Yay! 🎉**

## 📺 Demo

### Minimal Slash Command Interface

The Minimal Slash commands allows users fetch repository details such as issues, pull requests and contributors and share them on the channel. This feature can be a lifesaver while trying to send repository details on a channel and focusing the conversation around recent issues and pull requests. 

- `/github Username/RepositoryName` will fetch an interactive message which lets you send - Repository Details, Recent Pull Requests, Recent Issues and Contributor List to the channee.
- `/github Username/RepositoryName repo` send repository details to the channel.
- `/github Username/RepositoryName issue` sends recent issues to the channel.
- `/github Username/RepositoryName pulls` sends recent pull requests to the channel.
- `/github Username/RepositoryName contributors`sends the list of repository contributors to the channel.



https://user-images.githubusercontent.com/70485812/189435287-1ae93110-6ba2-4dbc-ab2f-4774a76cecfd.mp4

### GitHub OAuth

In the GitHub App I have implemented the Authnetication mechanism using OAuth2. Here we have used the [GitHub OAuth](https://docs.github.com/en/developers/apps/building-oauth-apps/authorizing-oauth-apps) along with the [RocketChat Apps Oauth2 Client](https://developer.rocket.chat/apps-engine/adding-features/oauth2-client).     
- The users can login to their github accounts simply by entering the slash command : `/github login` and clicking on the `login` button.
- As soon as the user is logged in, they receive a message and they can now use all the features which require authorized users.
- The users are automatically logged out after a period of time and the token is deleted. This was done to ensure the scalability of the feature incase of inactive users and to remove old ouath tokens from the apps limited persistent storage. To achieve this we use the [RocketChat Apps Scheduler API](https://developer.rocket.chat/apps-engine/adding-features/scheduler-api).

https://user-images.githubusercontent.com/70485812/189439737-78e25abc-a78b-43da-af2f-21a6c061bc38.mp4

## Event Subscriptions

The Event Subscriptions feature of the GitHub App allows users to subscribe to repository events such as - new pull request, new issues, new starts etc. Whenever a susbcribed repository event takes place, the GitHub App bot will send a message on the susbcribed room to describe the event.
This feature uses [GitHub WebHooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks) and [regestering an API end point](https://developer.rocket.chat/apps-engine/sample-app-snippets/registering-api-endpoints) in the App.
- The susbcription modal can be triggered using `/github subscribe` command and then we can subscribe to multiple events for a repository.
- If multiple room subscribe to a repository, a single web hook is used and the different events are sent to different channels. This helps us avoid multiple requests to the server for the same event.
- For any new events which are added or deleted, the same web hook is updated keeping in mind the events which are susbcribed by different rooms.


https://user-images.githubusercontent.com/70485812/189442882-afc3950e-4581-4728-b8c3-0e77e40ee61f.mp4

## GitHub Search & Share

This feature was initially supposed to be an extension of the Slash Commands but we decided to make it a completely interactive experience. 
- The GitHub Search feature allows users to search github for issues and pull request using different filters such as labels, authors, state, milestones etc.
- Users can `Add` multiple search results and `Share` them on the channel along with a custom message.
- This features improves the overall developer collaboration and helps share resources on the go.


https://user-images.githubusercontent.com/70485812/189448516-e846c836-551f-438e-960a-7c956d6b624f.mp4

## Opening New Issues

The GitHub App allows users to open new issues from RocketChat. The `NewIssueModal` can be triggered by using `/github issue` and then entering the repository name in the launched modal.
- This feature enables the users to fetch the issue templates for a repository from github, choose any of the given templates and open new issues with labels, assignees and rest of the properties. 
- The most challenging part about this feature was to find a way to fetch the repository issue templates. 
- GitHub does not yet have an API to fetch issue templates, but they can be extremely important to maintain uniformity and seperate different types of issues. To solve this problem, we used the [GitHub Repository Content API](https://docs.github.com/en/rest/repos/contents). 
- The issue templates are stored under `./github/ISSUE_TEMPLATES` on any repository, so inorder to fetch the templates, we fetched all the files on that path, downloaded the code and prepoplated the `InputElement` with the selected template.
- If the files did not exist, we simply skipped the Template-Selection Modal.

https://user-images.githubusercontent.com/70485812/189451845-34437a50-1fc8-4360-8b64-d1beac7af277.mp4

## Assigning Issues

This features allows users to fetch repository issues and update the assignees on any issue. It also enables users to fetch and share multiple repository issues at a time. We can fetch and assign issues by using `/github issues` command and then entering the repository name.

https://user-images.githubusercontent.com/70485812/189450860-5847e585-059c-4bed-a988-d21c99734969.mp4

## Pull Request Reviews 

This feature allows users to review and merge pull requests inside RocketChat.

- Pull Request data can be viewed either by using the `/github search` method and finding the pull reuqest or if the pull request number is known, we can simply use the slash command `/github Username/RepositoryName pulls pullNumber`.
- The pull request file changes, diffs, mergeaibility etc can also be seen. 
- A user can also see all the existing comments on the pull request and add new comments to the pull request directly from Rocket.Chat.
- While merging any pull request, the user can use any of the three methods - merge, rebase, squash.
- The user can also add a commit title and commit message while merging the pull request.
- Inorder to review the code changes, we intigrated a Code Editor component to fuselage and extended the component to be the ui-kit and made it re-usable for Rocket.Chat App developers by intigrating to the Rocket.Chat.Apps-engine. This was the most difficult feature and took a lot of research and effort to understand how  Rocket.Chat.App-engine, fuselage, ui-kit and Rocket.Chat interact with each other to render some new ui-block for different Rocket.Chat.Apps. 
- The Documentation including all the details of the Code Editor Integration can be found in the [project wiki](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting).



https://user-images.githubusercontent.com/70485812/189453201-a886b5b5-84d9-4621-9f8d-23311a980591.mp4







</div>
