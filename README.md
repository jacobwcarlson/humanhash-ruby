#humanhash-ruby

humanhash provides human-readable representations of digests. 

This is a Ruby port of lafncow's [fork](https://github.com/lafncow/humanhash)
of zacharyvoase's [original version](https://github.com/zacharyvoase/humanhash).Since I use the same compression technique as lafncow this is compatible with
his code, but not zacharvoase's.

## Examples

    [1] pry(main)> require 'humanhash'
    [2] pry(main)> digest = '7528880a986c40e78c38115e640da2a1'
    => "7528880a986c40e78c38115e640da2a1"
    [3] pry(main)> hasher = HumanHash::HumanHasher.new
    => #<HumanHash::HumanHasher:0x007fc67467f088
    [4] pry(main)> hasher.humanize(digest)
    => "five-magazine-mars-october"
    [5] pry(main)> hasher.humanize(digest, :words => 6)
    => "stream-zebra-comet-lemon-snake-october"
    [6] pry(main)> hasher.humanize(digest, :words => 6, :separator => '|')
    => "stream|zebra|comet|lemon|snake|october"
    [7] pry(main)> 10.times.map{hasher.uuid}
    => ["maryland-minnesota-avocado-yellow",
    "arizona-seventeen-skylark-december",
    "south-bulldog-foxtrot-saturn",
    "alaska-harry-network-beryllium",
    "south-shade-mars-paris",
    "maryland-avocado-floor-wyoming",
    "nine-emma-berlin-venus",
    "moon-mountain-pluto-fruit",
    "alaska-crazy-monkey-grey",
    "rugby-friend-fillet-island"]
    
## Caveats

Don't store the humanhash output, as its statistical uniqueness is only
256^words. Its intended use is as a human-readable (and, most
importantly, **memorable**) representation of a longer digest, unique enough
for display in a user interface, where a user may need to remember or verbally
communicate the identity of a hash, without having to remember a 40-character
hexadecimal sequence. Nevertheless, you should keep original digests around,
then pass them through `humanize()` only as you're displaying them.


## How It Works

The procedure for generating a humanhash involves compressing the input to a
fixed length (default: 4 bytes), then mapping each of these bytes to a word in
a pre-defined wordlist (a default wordlist is supplied with the library). This
algorithm is consistent, so the same input, given the same wordlist, will
always give the same output. You can also use your own wordlist, and specify a
different number of words for output.


## (Un)license

This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or distribute this
software, either in source code form or as a compiled binary, for any purpose,
commercial or non-commercial, and by any means.

In jurisdictions that recognize copyright laws, the author or authors of this
software dedicate any and all copyright interest in the software to the public
domain. We make this dedication for the benefit of the public at large and to
the detriment of our heirs and successors. We intend this dedication to be an
overt act of relinquishment in perpetuity of all present and future rights to
this software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF
CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <http://unlicense.org/>
