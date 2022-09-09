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


https://user-images.githubusercontent.com/70485812/189442882-afc3950e-4581-4728-b8c3-0e77e40ee61f.mp4




</div>
