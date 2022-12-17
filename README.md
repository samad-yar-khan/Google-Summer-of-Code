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
        <a href="#pushing-limits">Pushing Limits</a>&nbsp;&nbsp;&nbsp;
        <a href="#documentation">Documentation</a>&nbsp;&nbsp;&nbsp;
        <a href="#-mentors">Mentors</a>
    </code>
</p>

During Google Summer of Code 2022 I worked on the GitHub App for Rocket.Chat. This a GitHub integration for RocketChat which enables developers to use various GitHub features inside RocketChat channels.

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

The Minimal Slash commands allow users to fetch repository details such as issues, pull requests and contributors and share them on the channel. This feature can be a lifesaver while trying to send repository details on a channel and focusing the conversation around recent issues and pull requests. 

- `/github Username/RepositoryName` will fetch an interactive message which lets you send - Repository Details, Recent Pull Requests, Recent Issues and Contributor List to the channee.
- `/github Username/RepositoryName repo` send repository details to the channel.
- `/github Username/RepositoryName issue` sends recent issues to the channel.
- `/github Username/RepositoryName pulls` sends recent pull requests to the channel.
- `/github Username/RepositoryName contributors`sends the list of repository contributors to the channel.



https://user-images.githubusercontent.com/70485812/189435287-1ae93110-6ba2-4dbc-ab2f-4774a76cecfd.mp4

### 🔐 GitHub OAuth

In the GitHub App I have implemented the Authentication mechanism using OAuth2. Here we have used the [GitHub OAuth](https://docs.github.com/en/developers/apps/building-oauth-apps/authorizing-oauth-apps) along with the [RocketChat Apps Oauth2 Client](https://developer.rocket.chat/apps-engine/adding-features/oauth2-client).     
- The users can log in to their github accounts simply by entering the slash command : `/github login` and clicking on the `login` button.
- As soon as the user is logged in, they receive a message and they can now use all the features which require authorized users.
- The users are automatically logged out after a period of time and the token is deleted. This was done to ensure the scalability of the feature in case of inactive users and to remove old OAuth tokens from the apps limited persistent storage. To achieve this we use the [RocketChat Apps Scheduler API](https://developer.rocket.chat/apps-engine/adding-features/scheduler-api).

https://user-images.githubusercontent.com/70485812/189439737-78e25abc-a78b-43da-af2f-21a6c061bc38.mp4

### 🖇️ Event Subscriptions

The Event Subscriptions feature of the GitHub App allows users to subscribe to repository events such as - new pull requests, new issues, new starts etc. Whenever a subscribed repository event takes place, the GitHub App bot will send a message to the subscribed room to describe the event.
This feature uses [GitHub WebHooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks) and [regestering an API end point](https://developer.rocket.chat/apps-engine/sample-app-snippets/registering-api-endpoints) in the App.
- The subscription modal can be triggered using `/github subscribe` command and then we can subscribe to multiple events for a repository.
- If multiple rooms subscribe to a repository, a single webhook is used and the different events are sent to different channels. This helps us avoid multiple requests to the server for the same event.
- For any new events which are added or deleted, the same webhook is updated keeping in mind the events which are subscribed by different rooms.


https://user-images.githubusercontent.com/70485812/189442882-afc3950e-4581-4728-b8c3-0e77e40ee61f.mp4

### 🔍 GitHub Search & Share

This feature was initially supposed to be an extension of the Slash Commands but we decided to make it a completely interactive experience. 
- The GitHub Search feature allows users to search GitHub for issues and pull requests using different filters such as labels, authors, state, milestones etc.
- Users can `Add` multiple search results and `Share` them on the channel along with a custom message.
- This feature improves the overall developer collaboration and helps share resources on the go.


https://user-images.githubusercontent.com/70485812/189448516-e846c836-551f-438e-960a-7c956d6b624f.mp4

### 🚩 Opening New Issues

The GitHub App allows users to open new issues from RocketChat. The `NewIssueModal` can be triggered by using `/github issue` and then entering the repository name in the launched modal.
- This feature enables the users to fetch the issue templates for a repository from GitHub, choose any of the given templates and open new issues with labels, assignees and the rest of the properties. 
- The most challenging part about this feature was finding a way to fetch the repository issue templates. 
- GitHub does not yet have an API to fetch issue templates, but they can be extremely important to maintain uniformity and separate different types of issues. To solve this problem, we used the [GitHub Repository Content API](https://docs.github.com/en/rest/repos/contents). 
- The issue templates are stored under `./github/ISSUE_TEMPLATES` on any repository, so to fetch the templates, we fetched all the files on that path, downloaded the code and prepopulated the `InputElement` with the selected template.
- If the files did not exist, we simply skipped the Template-Selection Modal.

https://user-images.githubusercontent.com/70485812/189451845-34437a50-1fc8-4360-8b64-d1beac7af277.mp4

### 🏦 Assigning Issues

This feature allows users to fetch repository issues and update the assignees on any issue. It also enables users to fetch and share multiple repository issues at a time. We can fetch and assign issues by using `/github issues` command and then entering the repository name.

https://user-images.githubusercontent.com/70485812/189450860-5847e585-059c-4bed-a988-d21c99734969.mp4

### 📰 Pull Request Reviews 

This feature allows users to review and merge pull requests inside RocketChat.

- Pull Request data can be viewed either by using the `/github search` method and finding the pull request or if the pull request number is known, we can simply use the slash command `/github Username/RepositoryName pulls pullNumber`.
- The pull request file changes, diffs, mergeaibility etc can also be seen. 
- A user can also see all the existing comments on the pull request and add new comments to the pull request directly from Rocket.Chat.
- While merging any pull request, the user can use any of the three methods - merge, rebase, squash.
- The user can also add a commit title and commit message while merging the pull request.
- In order to review the code changes, we integrated a Code Editor component to fuselage and extended the component to be the ui-kit and made it reusable for Rocket.Chat App developers by integrating to the Rocket.Chat.Apps-engine. This was the most difficult feature and took a lot of research and effort to understand how  Rocket.Chat.App-engine, fuselage, ui-kit and Rocket.Chat interact with each other to render some new ui-block for different Rocket.Chat.Apps. 
- The Documentation including all the details of the Code Editor Integration can be found in the [project wiki](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting).



https://user-images.githubusercontent.com/70485812/189453201-a886b5b5-84d9-4621-9f8d-23311a980591.mp4


## 🚀 Contributions

### Pull Requests

<div align="center">

| PR Link   | Description  | Status | 
| :-----------: | :------------------------------------:| :------:|
| [PR #1](https://github.com/RocketChat/Apps.Github22/pull/1) | <b> [New] GitHub App Setup.</b> <br><br> <div align="left"> Highlights include:<ul><li>Slash Commands and interactive message to fetch repository data.</li><li>Fetching Pull Request Code Changes.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #7](https://github.com/RocketChat/Apps.Github22/pull/7) | <b>[New] Oath2 With RC Apps Scheduler and WebHooks Integration.</b> <br><br> <div align="left"> Highlights include:<ul><li>New OAuth2 Mechanism for GitHub Login</li><li>Using RC App Scheduler to Logout User after a period of time.</li><li>Added Repository subscription to all events ( isses, pull_request, push, deployment_status, star) using /github USERNAME/REPONAME subscribe.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #8](https://github.com/RocketChat/Apps.Github22/pull/8) | <b> [Feature] New Pull Request, Bug and Feature Request Templates. </b> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #11](https://github.com/RocketChat/Apps.Github22/pull/11) | <b> [Feature] Create GitHub Issues from Rocket.Chat channels </b>.<br><br> <div align="left"> Highlights include:<ul><li>Enabled users to select issue templates.</li><li>Adding labels, assignees etc while creating the issue.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #15](https://github.com/RocketChat/Apps.Github22/pull/15) | <b>[Feature] GitHub Search. </b><br><br> <div align="left"> Highlights include:<ul><li>Searching GitHub issues and pull requests using different filters such as author, labels, state etc.</li><li>Clubbing and Sharing multiple search results at once along with a custom message.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #16](https://github.com/RocketChat/Apps.Github22/pull/16) | <b>Improve User Experience - Update README. </b> <div align="left">| <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #18](https://github.com/RocketChat/Apps.Github22/pull/18) |[Feature] Merge PR and Comment on PRs. <br><br> <div align="left"> Highlights include:<ul><li>Merging Pull Request from Rocket.Chat along with custom commit message.</li><li> View Pull Request Comments and add New Comments to a Pull Request.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #20](https://github.com/RocketChat/Apps.Github22/pull/20) | [Feature] Assign Issues from RocketChat  <br><br> <div align="left"> Highlights include:<ul><li>Fetching repository issues and update issue assignees inside from Rocket.Chat</li><li>Sharing multiple issues at once.</li><div> | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40> |
| [PR #766](https://github.com/RocketChat/fuselage/pull/766) | (fuselage) [New] MediumMultilineInput and LargeMultilineInput Elements <br><br> <div align="left"> Highlights include:<ul><li>Added Adding a new `MediumMultilineInput` Component and a `LargeMultilineInput Component` to fuselage to support `code review` and `new issues` feature</li><div> | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40> |

</div>

### Issues
    
<div align="center">
    
| Issue Link   | Description  | Status | 
| :-----------: | :------------------------------------:| :------:|
| [ISSUE #10](https://github.com/RocketChat/Apps.Github22/issues/10) | [Feature] Create New GitHub Issues from Rocket.Chat  | <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #7](https://github.com/RocketChat/rocket.chat.app-poll/issues/12) | [Feature] GitHub Search integration enabling users to search for Issues and Pull Request | <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #3](https://github.com/RocketChat/rocket.chat.app-poll/issues/14) |[Feature] Improve User Experience| <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #10](https://github.com/RocketChat/rocket.chat.app-poll/issues/13) | [Feature] Issue Assignee Feature | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40> |
| [ISSUE #12](https://github.com/RocketChat/rocket.chat.app-poll/issues/17) | Pull Request Review : Merge And Comment on Pull Requests | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40>
| [ISSUE #765](https://github.com/RocketChat/fuselage/issues/765) | (fuselage) Larger Multiline Input Elements | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40>

</div>

## Pushing Limits

- In order to make this project a success we have pushed Rocket.Chat to the limit. To improve the collaboration and bring the GitHub conversations to Rocket.Chat we decided to add a Code Editor component to Rocket.Chat. This task was not so easy and required a lot of research.  
- Adding any new Component to the UIKit and making it re-usable for other Rocket.Chat App developers requires us to go through a series of additions in different repositories and understanding how [fuselage](https://github.com/RocketChat/fuselage/tree/develop/packages/fuselage), [ui-kit](https://github.com/RocketChat/fuselage/tree/develop/packages/ui-kit), [fuselage-ui-kit](https://github.com/RocketChat/fuselage/tree/develop/packages/fuselage-ui-kit) and [Rocket.Chat.Apps-engine](https://github.com/RocketChat/Rocket.Chat.Apps-engine) work together to render components inside [Rocket.Chat](https://github.com/RocketChat/Rocket.Chat). 
- The detailed documentation on how we went about adding a Code Editor to Rocket.Chat can be seen over here : [Pull Request Reviews : Integrating Code Editor with Syntax Highlighting](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting).
- To use the GitHub App the full potential, feel free to use the version of the GitHub App which uses the upgraded version of Rocket.Chat and other packages with the CodeEditor Component, update the dependencies to use modified versions of the Rocket.Chat.Apps-engine, fuselgae, ui-kit and fuselage-ui-kit.
   - [GitHub App with CodeEditor Component](https://github.com/samad-yar-khan/Apps.Github22/tree/demoApp).
   - [fuselage, ui-kit and fuselage-ui-kit with Code Editor integration](https://github.com/samad-yar-khan/fuselage/tree/CodeEditorInputAce).
   - [Rocket.Chat with intigrated Code Editor in the fuselage-ui-kit package](https://github.com/samad-yar-khan/Rocket.Chat/tree/CodeEditorComponent).
 
- GitHub App with the integrated CodeEditor can be used on this [hosted server](https://gh-app.rocketchat.digital/). This server uses the above-mentioned, upgraded versions of fuselage, ui-kit, Rocket.Chat.Apps-engine and Rocket.Chat.

## Documentation 

I have documented all of the features mentioned above in the [Project Wiki](https://github.com/RocketChat/Apps.Github22/wiki). This documentation can prove useful to all future Rocket.Chat contributors working on Rocket.Chat Apps, Apps-engine, fuselage or the ui-kit. 

    
<div align="center">

| **Feature** | **Documentation** |
|:--------------------|:-------------------|
| Authentication in Rocket.Chat Apps | [Authentication using RC OAuth2 Module and RC Apps Scheduler](https://github.com/RocketChat/Apps.Github22/wiki/Authentication-using-RC-OAuth2-Module-and-RC-Apps-Scheduler) |
| Adding new Elements to fuselage and UIKit | [Pull Request Reviews : Integrating Code Editor with Syntax Highlighting](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting) |
| Using WebHooks in Rocket.Chat Apps | [GitHub Event Subscriptions](https://github.com/RocketChat/Apps.Github22/wiki/GitHub-Event-Subscriptions) |
| GitHub Search (Using Rocket.Chat.App-engine persistent storage) | [GitHub Search and Share](https://github.com/RocketChat/Apps.Github22/wiki/GitHub-Search) |
| Opening New Issues (Fetching Issue Templates) | [Open New Issues from Rocket.Chat](https://github.com/RocketChat/Apps.Github22/wiki/Open-New-Issues-from-Rocket.Chat) |
| Pull Request Reviews (Using APIs and Modal in Rocket.Chat Apps)| [Merge Pull Requests and Add Comments](https://github.com/RocketChat/Apps.Github22/wiki/Merge-PRs-and-Add-Comments) |
| Assigning Issues (Using APIs, Modals and Persistent Storage in Rocket.Chat Apps) | [Assign and Sharing Issues from Rocket.Chat](https://github.com/RocketChat/Apps.Github22/wiki/Assigning-issues-from-Rocket.Chat) |

</div>

## 🎓 Mentors

A big big thank you to my mentors for their guidance before and throughout GSoC. 🙏

Rohan Lekhwani has been an inspiration throughout, his blogs and opensource work have been a lifesaver at each step of GSoC. I reached out to him over Linkedin last year and at the time I had no idea that he would end up being my mentor or that I would even be considered for GSoC'22. It would be accurate to say that I owe my GSoC'22 selection to him and his guidance. He has taught me how to own the project and juggle time between features to yield the best output possible.

Sing Li has taught me the importance of thinking beyond what has been done and pushing the limits even if the task at hand seems impossible. He has taught me the importance of communication and reaching out to people for guidance. His code reviews have made me a better developer and taught me how to think in terms of components and breaking down large problems into smaller problems and solving them one at a time. He motivated me to push myself and integrate the Code Editor inside Rocket.Chat, that became a highlighting feature for my project. This whole process was an enriching experience and can be considered a mini-GSoC Project of its own.

My mentors taught me things which will stay with me for life and I am beyond grateful for their guidance. Both of them have taught me how to think about the end user and make the product as scalable as possible. 

- **Rohan Lekhwani** - [GitHub](https://github.com/RonLek). [LinkedIn](https://www.linkedin.com/in/rohanlekhwani/)

- **Sing Li** - [GitHub](https://github.com/Sing-Li). [LinkedIn](https://www.linkedin.com/in/sing-li-119716139/)

Apart from my official Google Summer of Code Mentors, all Rocket.Chat community members have been extremely helful. 

I would like to thank Debdut Chakraborty for his amazing guidance and for helping me since my early days at Rocket.Chat. He spent hours to help me host the Rocket.Chat server with the modified fuselage, ui-kit and Apps-engine and without him my Demo at the Rocket.Chat GSoC'22 Demo day would not have been possible ❤️. Checkout the hosted server [over here](https://gh-app.rocketchat.digital/home).Feel free to reach out to him and tell him he's awesome !

- **Debdut Chakraborty** - [GitHub](https://github.com/debdutdeb). [LinkedIn](https://www.linkedin.com/in/debdut-chakraborty/)

## 💬 Connect With Me    

I am a senior year engineering student at Netaji Subhas University of Technology, Delhi. I am interested in Full Stack development and have been a contributor at Rocket.Chat since January 2022.

Want to discuss about GSoC / Rocket.Chat / Open-source ? Let's connect!

<div align="center">

| **Student** | Samad Yar Khan |
|:--------------------|:-------------------|
| **Organization** | [Rocket.Chat](https://rocket.chat/) |
| **Project** | [GitHub App](https://summerofcode.withgoogle.com/programs/2022/projects/dzvkQrUI) |
| **GitHub** | [@samad-yar-khan](https://github.com/samad-yar-khan) |
| **LinkedIn** | [samad-yar-khan](https://www.linkedin.com/in/samad-yar-khan/) |
| **Email** | <a href="mailto:smdyarkhan123@gmail.com">smdyarkhan123@gmail.com</a> |
| **Rocket.Chat** | [samad.khan](https://open.rocket.chat/direct/samad.khan) |
       
</div>

</div>
