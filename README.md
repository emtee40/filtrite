## filtrite
filtrite is a project for generating filter lists for [Bromite](https://www.bromite.org/).
See the page about [Custom Ad Block Filters](https://www.bromite.org/custom-filters) for more info.

# Lists
You can choose any list from below, copy the link and add it in Bromite by going to settings > AdBlock settings, then setting Filters URL to the one you just copied.

Here's a list:


| Name  | Description  |
| ------ | ------|
| [Bromite Default](https://github.com/xarantolus/filtrite/releases/latest/download/bromite-default.dat) | Bromite [default filter list](https://github.com/bromite/filters), but generated by this tool |
| [Bromite Extended](https://github.com/xarantolus/filtrite/releases/latest/download/bromite-extended.dat) | The default list with additional annoyance blockers I use with [uBlock Origin](https://github.com/gorhill/uBlock) on Desktop |


These lists are regularly updated automatically using GitHub Actions.

**Note**: I'm not 100% sure if all list formats that are used are actually supported by the ruleset generation tool (as the output indicates some failures). If you have a comment on that, please open an issue :)

### Contributing
This program is designed in a way that allows easily adding new lists. 
If you have an idea for new lists & combinations, then feel free to open an issue or pull request to point it out.

To add a new list:

1. Choose a name, e.g. `example-list`
2. Create a file `lists/example-list.txt` that contains all URLs. It should look like this:
```
# Comments and empty lines are allowed
# List one URL per line:
https://...
https://...

# This won't work, only put either a comment or an URL in one line, not both
http://  # Comment on URL
```
3. Save your file
4. Update [`generate.sh`](generate.sh) to include your entry:
```bash
...

echo "::group::List: example-list"
log "Start generating example-list"
# Syntax: ./filtrite <input list> <output>
# Make sure that your output has a `.dat` suffix
./filtrite lists/example-list.txt dist/example-list.dat
echo "::endgroup::"

...
```
6. Link your filter list in the README, using this URL: `https://github.com/xarantolus/filtrite/releases/latest/download/{YOUR FILENAME}.dat`. Replace `{YOUR FILENAME}` with the filename of the `.dat` file.
7. Create a pull request

Please also note that the script must be run on `linux/amd64` because `deps/ruleset_converter` is compiled for that.
