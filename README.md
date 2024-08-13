# Reward Rally - Platform that leverages gaming techniques to motivate user participation, engagement, and collaboration.

- [Prerequisites](#Prerequisites)
- [Usage](#usage)
- [Installation](#Installation)
- [Usage](#Usage)
- [License](#License)

# Prerequisites

### Reward Rally Account:

To register for an account on Reward Rally, Please reach out to us via phone call (+91 8925841838) or send an email to the specified email address contact@rewardrally.in Once you've contacted us, we will proceed to create an account for you to continue with the process.

Reward Rally Account:

- Your organization name
- Organisation Email address
- Username
- Phone number

We will generate a client Id and secret key for your organization. The users you provide should be the individuals who will be accessing the admin panel for configuration purposes. We will create your an admin with the given phone number to access the Reward Rally account for your organization.

Please note that integration requires an active Reward Rally account, and you should have the necessary login credentials for your Reward Rally account.

## Installation

Install @theproindia/rewardrally with npm

```bash
npm install @theproindia/rewardrally
```

## Usage

- import `@theproindia/rewardrally ` in app.module.ts.
  Replace the client credentials in the below code.

  ```bash
  import { RewardRallyModule } from "@theproindia/rewardrally ";

  RewardRallyModule.forRoot({
      clientId: <ClientId>,
      clientSecret: <ClientSecret>,
    }),
  ```

- Place the following tag in your HTML file where you want the leaderboard to be rendered.Pass the required parameters such as userId and appId (Application Id).

  ```bash
   <reward-rally
   [userId]="userId"
   [applicationId]="appId"
   [menuColor]="'black'"
   >
   </reward-rally>
  ```

- import the rewardrally service in the ts file and also do Dependency Injection

  ```bash
  import { RewardRallyService } from "@theproindia/rewardrally";
  constructor(public rewardRallyService: RewardRallyService) {}
  ```

- Call the updateGameAction() function from RewardRallyService to update score in the user leaderboard.
  pass the required parameters such as userId and gameActionId.
  get the GameActionId via configuration panel.

  ```bash
  this.rewardRallyService.updateGameAction(
       userId,
       gameActionId,
       correspondingUserId (optional),
       correspondingUserApplicationId (optional)
     )
  ```

## Security Reporting

If you find a security issue with our libraries or services please report it to contact@rewardrally.in with as much detail as possible. We will contact you shortly upon receiving the information.

## License

Copyright (c) Peninsular Research Operation. All rights reserved.

## Contact

For questions, issues, or feedback, please contact contact@rewardrally.in