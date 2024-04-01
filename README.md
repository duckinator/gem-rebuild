# gem-rebuild (plugin)

The `gem rebuild` command allows you to build a gem and compare it to an existing `.gem` file, to see if they are identical.

This command provides a base for implementing [Reproducible Builds](https://reproducible-builds.org/) for Ruby gems.

## Installation

Install the gem by executing:

    $ gem install gem-rebuild

## Usage

General usage is:

    $ gem rebuild GEM_NAME GEM_VERSION

When `gem rebuild` succeeds, it prints the line `SUCCESS - original and rebuild hashes matched`.

However, when `gem rebuild` fails, it prints the line `FAILURE - original and rebuild hashes did not match`.

You can also specify `--diff` to compare the two files using [`diffoscope`](https://diffoscope.org/) on failure.

<details>
<summary>Example success</summary>

```
~/test$ git clone --quiet https://github.com/duckinator/okay.git
~/test$ cd okay
~/test/okay$ git checkout v12.0.3
HEAD is now at 40fe265 Merge pull request #16 from duckinator/bump-deps
puppy@orthrus:~/test/okay$ gem rebuild okay 12.0.3
Fetching okay-12.0.3.gem
Downloaded okay version 12.0.3 as /tmp/gem_rebuild20240130-73307-ai5jxs/old/okay-12.0.3.gem.
  Successfully built RubyGem
  Name: okay
  Version: 12.0.3
  File: okay-12.0.3.gem

Built at: 2024-01-01 08:05:03 EST (1704114303)
Original build saved to:   /tmp/gem_rebuild20240130-73307-ai5jxs/old/okay-12.0.3.gem
Reproduced build saved to: /tmp/gem_rebuild20240130-73307-ai5jxs/new/okay-12.0.3.gem
Working directory: /usr/home/puppy/test/okay

Hash comparison:
  c6017966f3498623910f9a4a7bfcbd98ebab881f0e1315491b3340afa2e20b1c      /tmp/gem_rebuild20240130-73307-ai5jxs/old/okay-12.0.3.gem
  c6017966f3498623910f9a4a7bfcbd98ebab881f0e1315491b3340afa2e20b1c      /tmp/gem_rebuild20240130-73307-ai5jxs/new/okay-12.0.3.gem

SUCCESS - original and rebuild hashes matched
~/test/okay$
```

</details>

<details>
<summary>Example failure</summary>

```
~/test/okay$ echo "# some change" >> lib/okay.rb
~/test/okay$ gem rebuild okay 12.0.3
Fetching okay-12.0.3.gem
Downloaded okay version 12.0.3 as /tmp/gem_rebuild20240130-73881-x2dknj/old/okay-12.0.3.gem.
WARNING:  open-ended dependency on cacert (>= 0) is not recommended
  use a bounded requirement, such as "~> x.y"
WARNING:  See https://guides.rubygems.org/specification-reference/ for help
  Successfully built RubyGem
  Name: okay
  Version: 12.0.3
  File: okay-12.0.3.gem

Built at: 2024-01-01 08:05:03 EST (1704114303)
Original build saved to:   /tmp/gem_rebuild20240130-73881-x2dknj/old/okay-12.0.3.gem
Reproduced build saved to: /tmp/gem_rebuild20240130-73881-x2dknj/new/okay-12.0.3.gem
Working directory: /usr/home/puppy/test/okay

Hash comparison:
  c6017966f3498623910f9a4a7bfcbd98ebab881f0e1315491b3340afa2e20b1c      /tmp/gem_rebuild20240130-73881-x2dknj/old/okay-12.0.3.gem
  8910ae67d46e9cccc59c2a2dd08b29ddf03ac703bc95bcc7f69e1722926def94      /tmp/gem_rebuild20240130-73881-x2dknj/new/okay-12.0.3.gem

FAILURE - original and rebuild hashes did not match
~/test/okay$
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and the created tag, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/duckinator/gem-rebuild. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [code of conduct](https://github.com/duckinator/gem-rebuild/blob/main/CODE_OF_CONDUCT.md).

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the gem-rebuild project's codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/duckinator/gem-rebuild/blob/main/CODE_OF_CONDUCT.md).
