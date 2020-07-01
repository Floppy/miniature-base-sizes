# Mini Base Size Dataset

This repository is intended as a definitive list of base sizes for miniature gaming.

If you're converting, proxying, or 3d printing, you need to know the correct
base size for the miniature you're working on. This isn't always readily available - for instance,
although [Games Workshop](https://www.games-workshop.com) list the base sizes on their boxes and individual store pages,
they don't publish a proper list that covers everything.

## How the dataset works

We use data from [BattleScribe](https://battlescribe.net/) as the source of which models should be listed for particular games.
Currently, the repository includes data for [Warhammer 40,000](https://warhammer40000.com/), but any game with [BattleScribe data](https://github.com/BSData/)
could be added.

Each game has a subdirectory, which contains CSV files based on the data from BattleScribe.
Each file has the same set of columns:

* `name` of the model
* `base_size` (in mm)
* `base_short_axis` size for non-round bases (in mm)
* `base_shape` should be one of "round", "oval", ["stadium"](https://en.wikipedia.org/wiki/Stadium_(geometry)), "square", "hex", "irregular", or "none"
* `notes` is for freeform text notes. If you need to include a comma, put this field in double quotes.

## How to contribute

The lists are incomplete. If you want to help, that would be great!

1. [Create a free GitHub account](https://github.com/join) if you don't already have one.
1. Find the file you want to edit in this repository. You should be able search for specific models if you want.
1. Edit the file by pressing the pencil icon in the top right corner of the file view.
1. Make the changes to add your data (you need to edit the CSV text by hand for now, sorry).
1. Enter a commit message at the bottom, explaining what you added.
1. Hit "Propose Changes"

This will open a [Pull Request](https://github.com/Floppy/miniature-base-sizes/pulls) with your new data in it. Once we've checked it, we'll merge it into the main dataset. The data is automatically tested to make sure it's in the right format. If there's anything wrong, we'll let you know.

### Adding a new game

This is a bit more complex and involves using `git` and `ruby`. If you're OK with that:

1. Fork and clone the repo
1. Add the relevant battlescribe dataset as a submodule in `source_data`, using `git submodule add git@github.com:BSData/your-game.git`
1. Run `bundle install` to install the dependencies. You'll need `ruby` 2.7.1 installed.
1. Run `rake regenerate:all`. This will generate blank CSV data based on the BattleScribe data in a new top-level directory. All existing data will be overwritten, so discard any changes made that you don't want.
1. Copy `schema.json` from an existing subdirectory into the newly created directory for your game.
1. Customise the schema if you want to. For instance, you could change the valid base type list to suit your game.
1. Run `bundle exec cid validate` to make sure the csv files are generated properly.
1. Send a pull request.

## Ownership and Copyright

The authors of this dataset make no claim on ownership of any of the data, we're just collecting information that's already out there.

All copyrighted terms in this repository remain the property of their owners.