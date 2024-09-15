# MineCrash Solutions

This repository contains the JSON files used by MineCrash to solve errors submitted to it. Having them in a repository allows easy editing and pull requests.

## Requesting a solution to be added

You may request a solution to be added so we can provide the solution in the future. We do not solve and provide support for anything as of now so please only request a solution to be added if you already know how to solve it. We can then create a solution to help people who encounter the same issue. To request a solution you must provide information on the cause, including any warnings, errors or crashes, and how to solve it. If you are handy with REGEX you can attempt to make a contribution with a Pull Request, check the `Contributing` section further down.

## Solution Types

There are three different solution types MineCrash has. This is to help sort them into different categories. These are all found in their respective directories inside the `solutions/` directory.

### Warning

A warning is as it says. It checks for any possible warning inside the error, does not need to be related to any errors/crashes. A warning simply *warns* that there could be issues in the future that may occur if it is not fixed.

### Error

This is classified as when an error occurs that does not stop the server from being usable by any of its players. An error may affect a certain part of gameplay (e.g. A custom GUI errors when an item is clicked, resulting in nothing happening for the player) but it does not stop the server from functioning.

### Crash

A crash is an error that causes the server to stop functioning. It can be through the server freezing or hanging, sudden crashes where the server does not go through the normal shutdown steps, whether it is instant or delayed, or soft crashes where the server calls 'stop' on itself and shuts down while running all the normal steps, like saving data. Only one crash can be found per input, as the crash shuts the server down.

## FAQ

### Do you accept Java errors unrelated to Minecraft?

Minecraft (Java Edition) is made with the Java programming language so we kind of have to. Anyone can make plugins or mods for the game which people can end up getting errprs from.

### How does it work?

This is something outside of the scope for this repository. Please go and check out the repository for the backend of this service https://github.com/Eimer-Archive/MineCrashService/

### Is this limited to Minecraft or Java errors?

No, this uses REGEX to search for specific matches in the text. Logs for different games or programs are usually in plain text files so solutions for anything else can easily be added.

### Do or will you accept solutions for non Minecraft or Java errors?

No, currently we do not. We are focused towards providing solutions for the Minecraft community, you are free to fork this project and add your own solutions for anything you would like though!

## Contributing

Anyone may contribute as this is an open project trying to help people.

### Structure

All of the solutions go inside the `solutions/` directory. From there, there are directories for each solution type, `warning`, `error` and `crash`. Currently all the solution files go inside these directories.

### Template

There is a basic template example for creating new solutions `template.json`.

`error` is the title of the error that appears on the solution. Such as `Port is already in use`.

The `matches` array is a list of Regular Expressions that each get run to check if the input is in need of that specific solution. The matches run as an `OR` check, so only one of them need to find a match for it to be marked as having a solution found.
One example
```json
"matches": [
  "Error 1",
  "Error 2"
]
```
This will match if EITHER `Error 1` or `Error 2` is found in the input, as they will both has the same solution or are both possible symptoms of the same issue. Sometimes a full log is not submitted by the user so this can be useful.

`arguments` contains the arguments for possible related information. It is made up of the identifier and the Regular Expression to find the related information. The identifier is used in the `solution` so that the information can be passed to that specific location. The Regular Expression is used to find the related information that can be relayed back. One example is extracting the name of the plugin or mod that is responsible for the issue.
```json
"arguments": {
  "0": "Could not load 'plugins\\/([^']+)"
}
```
This example extracts the plugins name from the provided input as the argument `0`. The argument name can be any string.

The `solution` is the solution for the particular warning, error or crash that is encountered. It explains any possible steps to solve the problem. It uses `arguments` to provide more context and point the user in the right direction, such as pointing out the plugin or mod that is causing the problem. To use can argument a `%` is placed before the argument name, like `%0`.
