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

### Minimal  Slash Command Interface

</div>
