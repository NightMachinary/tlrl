## DEPRECATED

I have reimplemented a URL-to-Kindle CLI application in my scripts (Currently https://github.com/NightMachinary/.shells but I plan to move the scripts to their own repo). It's the function called `tlrl-ng` in `scraping.zsh`. It uses already established tools (e.g., pandoc, calibre, mercury-parser, curl, ...) to do a stable, reliable, maintainable job. I no longer plan to use tlrl, as it is buggy, slow to install via `cargo`, and hard to hack on. `tlrl-ng` maintains backwards-compatibility with `tlrl` and can be used as a drop-in replacement. (Though its verbosity is different from `tlrl`.)

## Differences from the Original

I have forked this from [sodiumjoe](https://github.com/sodiumjoe/tlrl).
Look at the commits to see what I have changed, but here is a partial summary:

* Uses local [mercury-parser](https://github.com/postlight/mercury-parser) (so it should be available on your PATH)(I have not removed the code for reading the API from config, but you can just put jibberish in it now :D)

  Basically just do this:

  ```
  # Install Mercury globally
  yarn global add @postlight/mercury-parser
  #   or
  npm -g install @postlight/mercury-parser
  ```

* Supports --prefix-title.

tl;rl
=====

Send a web page to your kindle for reading later from the command line.

## Installation

Install rust and cargo (Just google them). Then use:

`cargo install --git https://github.com/NightMachinary/tlrl/`

## Configuration

Read [the differences from the original](#differences-from-the-original) at the top first.

1. [Get an api key for the Mercury API](https://mercury.postlight.com/web-parser/).
2. [Create an application-specific password for gmail](https://myaccount.google.com/apppasswords).
  * Select App -> Other (custom)
3. Make sure you have a kindle email address set up.
  * [Go to Amazon](https://www.amazon.com)
  * -> Account & Lists
  * -> Your Content and Devices
  * -> Settings
  * -> Personal Document Settings
  * -> Send-to-Kindle E-Mail Settings
4. Make sure you have a kindle approved sender email address.
  * -> Approved Personal Document E-mail List
5. Create a `~/.tlrl.json` file:

```json
{
  "mercury_token":"from step 1",
  "gmail_application_password": "from step 2",
  "kindle_email": "from step 3",
  "gmail_username": "from step 4",
}
```

## Usage

```
$ tlrl <url>
```

This helper function was useful in the days that we used the remote Mercury API (usage: `retry tlrl ...`):

```
retry () {
	until "$@"
	do
		echo Retrying \'"$*"\' "..." >&2
		sleep 1
	done
}
```

## Help

```
$ tlrl -h
```
