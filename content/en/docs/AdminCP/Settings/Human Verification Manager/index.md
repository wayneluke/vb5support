---
title: Human Verification Manager
slug: human_verification_manager
weight: 40
---

## Image

Image verification presents a series of distorted numbers and letters that the user is required to enter. Either GD2 or ImageMagick support is required from your PHP server in order to use this option. This is the classic option that most users are accustomed to encountering. Disabled users will be blocked with this option.

## Question and Answer

Question & Answer verification employs a random question challenge with a predefined set of appropriate answers. The questions and answers must be defined by the administrator. This allows the questions to be tailored to the forum content as well as preventing a common set of questions from becoming prevalent across a large section of vBulletin forums. Maintaining unique questions is required for this option to be successful. This option should be accessible to any impaired user that is able to use the Internet.

## ReCaptcha v2

reCAPTCHA™ employs a verification provided by Google. This system validate users with the "I'm not a robot" checkbox.

This option requires the cURL library to be installed within PHP.

## Human Verified Actions
Human Verification will be required for the selected actions where the user's usergroup permission **Require Human Verification for Configured Actions** is selected.

## Bypassing Human Verification

Each usergroup can be configured to bypass Human Verification. To do this, go Usergroups → Usergroup Manager in the AdminCP. Edit the Usergroup that you want to update and then set the "_Require Human Verification on Configured Actions_" permission to No.
