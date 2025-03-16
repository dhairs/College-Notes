
## Memory Amounts

Because we basically do everything in binary, and everything is in powers of 2, it only makes sense if the memory we represent is also in powers of 2. It makes alignment easier, and also just makes use of all the bits we have. For this reason, we redefine certain prefixes to make more sense in the base-2 space:

#### Kilobyte (KB)
$1\text{KB}=10^3$ bytes.

#### Megabyte (MB)
$1\text{MB}=10^6$ bytes.

#### Gigabyte (GB)
$1\text{GB}=10^9$ bytes.

#### Kibibyte (KiB)
Replaces Kilobyte (KB), which is defined as $10^3$ bytes.

$1\text{KiB}=2^{10}\text{ bytes}$.

#### Mebibyte (MiB)
Replaces Megabyte (MB), which is defined as $10^6$ bytes.

$1\text{MiB}=2^{20}\text{ bytes}$.

#### Gibibyte (GiB)
Replaces Gigabyte (GB), which is defined as $10^9$ bytes.

$1\text{GiB}=2^{30}\text{ bytes}$.

This pattern continues so on:
#### The Pattern (XiB)
Replaces XB, which can be defined as
$10^\text{multiple of 3}$ bytes.

To derive the version we're looking for: 
$$
10^{3x}\text{ XB}=2^{10x}\text{ XiB}
$$
