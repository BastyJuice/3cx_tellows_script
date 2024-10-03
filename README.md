# 3CX Call Handling Script for Tellows Live API

This script is designed to integrate with the **3CX phone system** to detect and handle spam calls using the **Tellows API**. It includes functionality for whitelisting and blacklisting specific numbers, routing calls based on spam scores, and logging events.

## Key Features

1. **Tellows Spam Detection**:
   - Queries the Tellows API to get a spam score for the incoming call.
   - If the spam score exceeds a configurable threshold, the call is considered spam and routed accordingly.

2. **Whitelist**:
   - A list of phone numbers that will always be treated as **non-spam**, regardless of the Tellows score.
   - Calls from these numbers are automatically routed to the originally dialed destination.

3. **Blacklist**:
   - A list of phone numbers that will always be treated as **spam**, regardless of the Tellows score.
   - Calls from these numbers are automatically routed to a predefined spam extension.

4. **Call Routing**:
   - **Non-spam calls** are routed to the originally dialed destination.
   - **Spam calls** are routed to a predefined internal spam extension.
   - Configurable routing timeout to handle call forwarding and routing failures.

5. **Logging**:
   - Logs important events, including spam detection, routing actions, and errors, to a log file.
   - Logging can be enabled or disabled through the `enableLogging` variable.

6. **Configuration Options**:
   - **API Keys**: Replace with your Tellows API key and partner ID. https://blog.tellows.de/2011/07/tellows-api-fur-die-integration-in-eigene-programme/
   - **Whitelist and Blacklist**: Specify comma-separated phone numbers in the variables `whitelist` and `blacklist`.
   - **Log File Path**: Define the log file location in the `logFileName` variable.
   - **Spam Threshold**: Configure the spam score threshold that triggers spam call handling.

## Configuration

1. **API Variables**:
   - `tellowsApiKey`: Your Tellows API key.
   - `tellowsPartnerID`: Your Tellows partner ID.

2. **Phone Number Management**:
   - `whitelist`: Comma-separated list of phone numbers that are always treated as non-spam.
   - `blacklist`: Comma-separated list of phone numbers that are always treated as spam.

3. **Logging**:
   - `enableLogging`: Set to `true` or `false` to enable or disable logging.
   - `logFileName`: Path to the log file where events will be recorded.

4. **Spam Threshold**:
   - `tellowsThreshold`: Spam score threshold (e.g., a score of 5 or higher will be treated as spam).

5. **Internal Spam Extension**:
   - `internalSpamExtension`: The internal extension number to which spam calls are routed.

## How It Works

1. The script intercepts incoming calls and checks if the caller’s number is in the whitelist or blacklist.
2. If the number is whitelisted, the call is routed to the originally dialed number.
3. If the number is blacklisted, the call is routed to the internal spam extension.
4. If the number is not on either list, the Tellows API is queried for a spam score.
5. Based on the Tellows score:
   - If the score exceeds the defined threshold, the call is treated as spam and routed to the spam extension.
   - If the score is below the threshold, the call is treated as non-spam and routed to the originally dialed number.
6. Logging captures all key events, errors, and call routing details.

## Setup

1. Replace the placeholder values (API keys, phone numbers, etc.) with your actual data.
2. Adjust the spam threshold, timeout values, and other configurable settings as needed.
3. Deploy the script in your 3CX environment and monitor the log file for events and troubleshooting.

## Notes

- The Tellows API key and partner ID are required for spam detection.
- Ensure that the `logFileName` path is accessible and writable by the script.
- Test the script thoroughly in a safe environment before deploying it in production.
