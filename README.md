WorldGreenCoin Core integration/staging tree
=====================================

https://www.worldgreencoin.com

Copyright (c) 2009-2018 Bitcoin Core Developers

Copyright (c) 2014-2018 WorldGreenCoin Core Developers

What is WorldGreenCoin?
----------------

WorldGreenCoin is an experimental new digital currency that enables instant payments to
anyone, anywhere in the world. WorldGreenCoin uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. WorldGreenCoin Core is the name of open source
software which enables the use of this currency.

WorldGreenCoin first started in January 2014 as a variant of Litecoin using Scrypt as
the Proof-of-Work (PoW) hash algorithm.
 - 1 minute block target
 - 100,000 coins per block
 - subsidy halves every 500,000 blocks
 - subsidy halves every 50,000 blocks starting at block 140,000
 - difficulty retarget: every block using Kimoto's gravity well


On 2nd August 2014 at block 260,800 WorldGreenCoin transitioned to its own original Proof-of-Stake-Velocity (PoSV)
algorithm which replaced Proof-of-Work (PoW).
 - 1 minute block target
 - just under 27 billion mined in PoW phase
 - 5% annual interest in PoSV phase
 - difficulty retarget: every block using Kimoto's gravity well
 - white paper: http://www.worldgreencoin.com/papers/PoSV.pdf
 - FAQs paper: http://www.worldgreencoin.com/papers/PoSV_FAQ.pdf

On December 2015 work commenced on porting directly from Bitcoin v0.9 whilst maintaining the original functionality.
 - allowing for better maintainabilty
 - monitoring of upstream features
 - improved code consistency and sharing

For more information, as well as an immediately useable, binary version of
the WorldGreenCoin Core software, see http://www.worldgreencoin.com

License
-------

WorldGreenCoin Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see http://opensource.org/licenses/MIT.

Development process
-------------------

Developers work in their own trees, then submit pull requests when they think
their feature or bug fix is ready.

If it is a simple/trivial/non-controversial change, then one of the WorldGreenCoin
development team members simply pulls it.

If it is a *more complicated or potentially controversial* change, then the patch
submitter will be asked to start a discussion (if they haven't already) on the relevant forum channel.

The patch will be accepted if there is broad consensus that it is a good thing.
Developers should expect to rework and resubmit patches if the code doesn't
match the project's coding conventions (see [doc/coding.md](doc/coding.md)) or are
controversial.

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/worldgreencoin-project/worldgreencoin/tags) are created
regularly to indicate new official, stable release versions of Bitcoin.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test. Please be patient and help out, and
remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write unit tests for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run (assuming they weren't disabled in configure) with: `make check`

Every pull request is built for Windows, Linux and OSx on a dedicated server,
and unit and sanity tests are automatically run. The binaries produced may be
used for manual QA testing — a link to them will appear in a comment on the
pull request posted by [BitcoinPullTester](https://github.com/BitcoinPullTester). See https://github.com/TheBlueMatt/test-scripts
for the build/test scripts.

### Manual Quality Assurance (QA) Testing

Large changes should have a test plan, and should be tested by somebody other
than the developer who wrote the code.
See https://github.com/bitcoin/QA/ for how to create a test plan.

Translations
------------

Changes to translations as well as new translations can be submitted to
[Bitcoin Core's Transifex page](https://www.transifex.com/projects/p/bitcoin/).

Periodically the translations are pulled from Transifex and merged into the git repository. See the
[translation process](doc/translation_process.md) for details on how this works.

**Important**: We do not accept translation changes as github pull request because the next
pull from Transifex would automatically overwrite them again.

Development tips and tricks
---------------------------

**compiling for debugging**

Run configure with the --enable-debug option, then make. Or run configure with
CXXFLAGS="-g -ggdb -O0" or whatever debug flags you need.

**debug.log**

If the code is behaving strangely, take a look in the debug.log file in the data directory;
error and debugging message are written there.

The -debug=... command-line option controls debugging; running with just -debug will turn
on all categories (and give you a very large debug.log file).

The Qt code routes qDebug() output to debug.log under category "qt": run with -debug=qt
to see it.

**testnet and regtest modes**

Run with the -testnet option to run with "play worldgreencoins" on the test network, if you
are testing multi-machine code that needs to operate across the internet.

If you are testing something that can run on one machine, run with the -regtest option.
In regression test mode blocks can be created on-demand; see qa/rpc-tests/ for tests
that run in -regest mode.

**DEBUG_LOCKORDER**

WorldGreenCoin Core is a multithreaded application, and deadlocks or other multithreading bugs
can be very difficult to track down. Compiling with -DDEBUG_LOCKORDER (configure
CXXFLAGS="-DDEBUG_LOCKORDER -g") inserts run-time checks to keep track of what locks
are held, and adds warning to the debug.log file if inconsistencies are detected.
