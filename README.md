﻿![Reward Rally](https://rewardrally.in/assets/favicon.svg) ![Angular](https://v17.angular.io/assets/images/logos/angular/logo-nav@2x.png)

# Reward Rally - Angular NPM Integration Documentation

## Overview

Reward Rally is a platform that leverages gaming techniques to motivate user participation, engagement, and collaboration.

## Scope

This document provides detailed instructions for integrating Reward Rally into a Angular application. It is intended for developers and technical teams who need to implement Reward Rally's gamification and leaderboard features.

## Audience

- Developers integrating Reward Rally into their Angular applications.
- Technical teams responsible for configuring and maintaining the integration.

## Prerequisites

- Reward Rally account.
- Credentials needed for integration.

## Integration Steps

### Installation

Install the Reward Rally Angualar NPM package:

```bash
$ npm i @theproindia/rewardrally
```

## Usage

Next, you need to import the RewardRallyModule into your Angular application. Open your `app.module.ts` file and configure the module as follows:

```bash
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
 declarations: [
   AppComponent ],
 imports: [
   RewardRallyModule.forRoot({
     clientId: <ClientId>,
     clientSecret: <ClientSecret>,
   }),
 ],
 providers: [],
 bootstrap: [AppComponent],
})

export class AppModule {}
```

### Parameters:

- `clientId` (string): Client credential provided by the Reward Rally team.
- `clientSecret` (string): Client credential provided by the Reward Rally team.

## Render Leaderboard

Place the following tag in your HTML file where you want the `leaderboard` to be rendered.

```bash
   <reward-rally
   [userId]=<userId>
   [applicationId]=<appId>
   [menuColor]=<black>
   >
   </reward-rally>
```

### Parameters:

- `userId` (string): Unique User ID from your client application.
- `applicationId` (string): Application ID configured in the Reward Rally admin panel.

## Create User

This section provides instructions on how to create a new user in the Reward Rally system using the `addUser` function.

The `addUser` function is used to register a new user in the Reward Rally system. This function requires specific user details to be provided and returns a response with information about the newly created user.

## Function Syntax

### Component Code (`create-user.component.ts`)

```bash

import { Component } from '@angular/core';
import { RewardRallyService } from '@theproindia/rewardrally';

@Component({
  selector: 'app-create-user',
  templateUrl: './create-user.component.html',
})
export class CreateUserComponent {
  constructor(
    private rewardRallyService: RewardRallyService
  ) {}

  onSubmit(): void {
      const user ={
      userId: <userId>,
      userName: <userName>,
      application: <application>,
    }
      this.rewardRallyService.addUser(user)
        .then(() => {
          this.message = 'User created successfully!';
        })
        .catch(error => {
          this.message = 'Error creating user: ' + error.message;
        });

  }
}

```

### Component Template (`create-user.component.html`)

```bash

    <button type="submit">Create User</button>

```

## Update User

This section provides instructions on how to update an existing user in the Reward Rally system using the updateUser function.

The updateUser function is used to modify the details of an existing user in the Reward Rally system. This function requires specific user information and identifiers to be provided and returns a response indicating the success or failure of the update operation.

## Function Syntax

### Component Code (`update-user.component.ts`)

```bash
import { RewardRallyService } from '@theproindia/rewardrally';

const user = {
  userId:<userId>,
  userName: <userName>,
  application: [<application>],
  profileImageUrl: <profileImageUrl>
};

const userInput = {
  userId: <userId>,
  appId: <appId>
};

this.rewardRallyService.updateUser(user, userInput)
  .then(response => {
    console.log('User updated successfully:', response);
  })
  .catch(error => {
    console.error('Error updating user:', error.message);
  });

```

### Parameters:

`user`: An object containing the details to be updated. The User object can include:

- `userId` (string, optional): The ID of the user.
- `userName` (string, optional): The new name of the user.
- `application` (string[], optional): The list of application IDs associated with the user.
- `profileImageUrl` (string, optional): The URL of the user's profile image.

`userInput`: An object containing identifiers for the update. The UserInput object includes:

- `userId` (string): The ID of the user to update.
- `appId` (string): The application ID related to the update.

## Add Users in Bulk

This section provides instructions on how to add multiple users to the Reward Rally system using the `addUsersAsList` function.

The `addUsersAsList` function allows you to register a list of users in the Reward Rally system in one operation. This function takes an array of user details and returns an Observable with information about the success or failure of the operation.

## Function Syntax

### Component Code (`create-user-list.component.ts`)

```bash

import { Component } from '@angular/core';
import { RewardRallyService } from '@theproindia/rewardrally';

@Component({
  selector: 'app-add-users',
  templateUrl: './add-users.component.html',
})
export class AddUsersComponent {
  constructor(private rewardRallyService: RewardRallyService) {}

  onSubmit(): void {
    const userList = [
      {
        userId: <user1>,
        userName: <User One>,
        application: [<app1>],
      },
      {
        userId: <user2>,
        userName: <User Two>,
        application: [<app2>],
      }
    ];

    this.rewardRallyService.addUsersAsList(userList)
      .subscribe({
        next: (response) => {
          console.log('Users added successfully:', response);
        },
        error: (error) => {
          console.error('Error adding users:', error.message);
        }
      });
  }
}


```

### Parameters:

- `userId` (string): The ID of the user.
- `userName` (string): The new name of the user.
- `application` (string[]): The list of application IDs associated with the user.

## Delete User

This section provides instructions on how to delete a user from the Reward Rally system using the `deleteUser` function.

he `deleteUser` function allows you to remove an existing user from the Reward Rally system. This function requires the user ID to be provided and returns a response indicating the success or failure of the deletion operation.

## Function Syntax

### Component Code (`delete-user.component.ts`)

```bash

import { Component } from '@angular/core';
import { RewardRallyService } from '@theproindia/rewardrally';

@Component({
  selector: 'app-delete-user',
  templateUrl: './delete-user.component.html',
})
export class DeleteUserComponent {
  message: string = '';

  constructor(private rewardRallyService: RewardRallyService) {}

  deleteUser(userId: string): void {
    this.rewardRallyService.deleteUser(userId)
      .then(response => {
        this.message = 'User deleted successfully!';
        console.log('Response:', response);
      })
      .catch(error => {
        this.message = 'Error deleting user: ' + error.message;
        console.error('Error:', error.message);
      });
  }
}


```

### Parameters:

- `userId` (string): The ID of the user.

## Get User by Application ID

This section provides instructions on how to retrieve user details from the Reward Rally system using the `getUserByAppId` function.

The `getUserByAppId` function allows you to fetch user details based on the user ID and application ID. This function requires both identifiers to be provided and returns a response with the user details.

## Function Syntax

### Component Code (`get-user.component.ts`)

```bash

import { Component } from '@angular/core';
import { RewardRallyService } from '@theproindia/rewardrally';

@Component({
  selector: 'app-get-user',
  templateUrl: './get-user.component.html',
})
export class GetUserComponent {
  userDetails: any = {};
  message: string = '';

  constructor(private rewardRallyService: RewardRallyService) {}

  getUser(userId: string, appId: string): void {
    this.rewardRallyService.getUserByAppId(userId, appId)
      .then(response => {
        this.userDetails = response;
        this.message = 'User details retrieved successfully!';
        console.log('User Details:', this.userDetails);
      })
      .catch(error => {
        this.message = 'Error retrieving user details: ' + error.message;
        console.error('Error:', error.message);
      });
  }
}


```

### Parameters:

- `userId` (string): The ID of the user.
- `application` (string[]): The list of application IDs associated with the user.

## Remove User Information

This section provides instructions on how to remove user information from local storage using the `removeUserInfo`.

The `removeUserInfo` function is used to clear user-related data stored in local storage. This function does not require any parameters and will remove the specified user information from local storage.

## Function Syntax

### Component Code (`remove-user-info.component.ts`)

```bash

import { Component } from '@angular/core';
import { RewardRallyService } from '@theproindia/rewardrally';

@Component({
  selector: 'app-remove-user-info',
  templateUrl: './remove-user-info.component.html',
})
export class RemoveUserInfoComponent {
  message: string = '';

  constructor(private rewardRallyService: RewardRallyService) {}

  removeUserInfo(): void {
    this.rewardRallyService.removeUserInfo();
    this.message = 'User information removed from local storage.';
  }
}


```

## Updating a Game Action

This section provides instructions on how to trigger a gameaction in the Reward Rally system using the `updateGameAction` function.

To trigger a game action, use the `updateGameAction` function provided by the Reward Rally package. This function allows you to notify the system of actions performed by a user.

## Function Syntax

### Component Code (`example.component.ts`)

```bash

import { Component } from '@angular/core';
import { RewardRallyService } from 'rewardrally';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
})
export class ExampleComponent {

  constructor(private rewardRallyService: RewardRallyService) { }

  async onUpdateGameAction(): Promise<void> {
    try {

      await this.rewardRallyService.updateGameAction(
      <userId>
      <gameactionId>,
      <correspondingUserId>(optional),
      <correspondingUserApplicationId>(optional)
      );

      console.log('Game action triggred successfully');
    } catch (error) {
      console.error('Error updating game action:', error);
    }
  }
}

```

### Component Template (`example.component.html`)

```bash

<div>
  <button (click)="onUpdateGameAction()">Update Game Action</button>
</div>

```

### Parameters:

- `userId` (string): The ID of the user performing the action. This is a required parameter.
- `gameActionId` (string): The specific action being reported. This should be a predefined action ID or type.
- `correspondingUserId` (string, optional): Works Only with Rival Points configuration
- `correspondingUserApplicationId` (string, optional): Works Only with Rival Points configuration

## Security Reporting

If you find a security issue with our libraries or services, please report it to [contact@rewardrally.in](mailto:contact@rewardrally.in) with as much detail as possible. We will contact you shortly upon receiving the information.

## License

Copyright (c) Peninsular Research Operation. All rights reserved.

## Contact

For questions, issues, or feedback, please contact [contact@rewardrally.in](mailto:contact@rewardrally.in).
