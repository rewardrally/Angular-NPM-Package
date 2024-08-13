![Reward Rally](https://rewardrally.in/assets/favicon.svg)

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
   StarRatingModule.forRoot(),
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
   [userId]="userId"
   [applicationId]="appId"
   [menuColor]="'black'"
   >
   </reward-rally>
```

### Parameters:

- `userId` (string): Unique User ID from your client application.
- `applicationId` (string): Application ID configured in the Reward Rally admin panel.

## Create User with Reward Rally

This section provides instructions on how to create a new user in the Reward Rally system using the `addUser` function.

The `addUser` function is used to register a new user in the Reward Rally system. This function requires specific user details to be provided and returns a response with information about the newly created user.

## Function Syntax

## Component Code (`create-user.component.ts`)

```bash

import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { RewardRallyService } from '@theproindia/rewardrally';

@Component({
  selector: 'app-create-user',
  templateUrl: './create-user.component.html',
})
export class CreateUserComponent {
  userForm: FormGroup;
  message: string = '';

  constructor(
    private fb: FormBuilder,
    private rewardRallyService: RewardRallyService
  ) {
    this.userForm = this.fb.group({
      userId: ['', Validators.required],
      userName: ['', Validators.required],
      application: ['', Validators.required],
    });
  }

  onSubmit(): void {
    if (this.userForm.valid) {
      const user = this.userForm.value;
      this.rewardRallyService.addUser(user)
        .then(() => {
          this.message = 'User created successfully!';
          this.userForm.reset();
        })
        .catch(error => {
          this.message = 'Error creating user: ' + error.message;
        });
    } else {
      this.message = 'Please fill out all required fields.';
    }
  }
}

```

## Component Template (`create-user.component.html`)

```bash

<div>
  <h2>Create User</h2>
  <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
    <label for="userId">User ID:</label>
    <input id="userId" formControlName="userId" />

    <label for="userName">User Name:</label>
    <input id="userName" formControlName="userName" />

    <label for="application">Application ID:</label>
    <input id="application" formControlName="application" />

    <button type="submit">Create User</button>
  </form>

  <p *ngIf="message">{{ message }}</p>
</div>

```

## Updating a Game Action

This section provides instructions on how to trigger a gameaction in the Reward Rally system using the `updateGameAction` function.

To trigger a game action, use the `updateGameAction` function provided by the Reward Rally package. This function allows you to notify the system of actions performed by a user.

## Function Syntax

## Component Code (`example.component.ts`)

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

## Component Template (`example.component.html`)

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
