# TickList

{% hint style="info" %}
Contains utility methods that aids in searching and sorting ticks from a Ticks list.



**GitHub File:** [tickList.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/utils/tickList.ts)
{% endhint %}

## Constructor

Private constructor that cannot be constructed.

## Methods

### validateList() - `public` `static`

Validates the list of ticks and throws if the list is invalid.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tickSpacing</td><td>number</td><td>The tick spacing. Used to validate correct tick spacing and check pool liquidity against the total net liquidity across ticks.</td></tr></tbody></table>

***

### isBelowSmallest() - `public` `static`

Checks if a given tick is below the lowest tick in the `ticks` array.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tick</td><td>number</td><td>The tick to check against the array.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = The provided tick is smaller than the lowest tick in the provided <code>ticks</code> array.<br><code>false</code> = The provided tick is larger than the lowest tick in the provided <code>ticks</code> array.</td></tr></tbody></table>

***

### isAtOrAboveLargest() - `public` `static`

Checks if a given tick is above or equal to the highest tick in the `ticks` array.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tick</td><td>number</td><td>The tick to check against the array.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = The provided tick is greater or equal to the largest tick in the provided <code>ticks</code> array.<br><code>false</code> = The provided tick is lower than the highest tick in the provided <code>ticks</code> array.</td></tr></tbody></table>

***

### getTick() - `public` `static`

Returns the tick that corresponds to the specified index number.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>index</td><td>number</td><td>The index number of the tick to search.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The tick that matches the given index number.</td></tr></tbody></table>

***

### binarySearch() - `private` `static`

Returns the largest tick index that is less than or equal to the specified tick.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tick</td><td>number</td><td>The tick to search for the largest tick that is less than or equal to this tick.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>The tick index that is less than or equal to the specified tick.</td></tr></tbody></table>

***

### nextInitializedTick() - `public` `static`

Returns the net initialized tick from the specified tick.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tick</td><td>number</td><td>The tick number that functions as the strating point for the search.</td></tr><tr><td>lte</td><td>boolean</td><td><code>true</code> = Searches for the next initialized tick that is less than or equal to the specified tick.<br><code>false</code> = Searches for the next initialized tick that is greater than the specified tick.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="tick.md">Tick</a></td><td>The next initialized tick from the specified tick.</td></tr></tbody></table>

***

### nextInitializedTickWithinOneWord() - `public` `static`

Searches the current and neighbouring words and returns the next initialized tick.&#x20;

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tick</td><td>number</td><td>The tick number that functions as the starting point for the search.</td></tr><tr><td>lte</td><td>boolean</td><td><code>true</code> = Searches for the next initialized tick that is less than or equal to the specified tick.<br><code>false</code> = Searches for the next initialized tick that is greater than the specified tick.</td></tr><tr><td>tickSpacing</td><td>number</td><td>The spacing between usable ticks.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>[number, boolean]</td><td>An array whose indexes contain the following values:<br><br><code>0</code> = The next initialized tick up to 256 ticks away from the current active tick. If the next initialized tick is not within ±256 ticks, the value returned will be the last uninitialized tick from the current active tick (currentTick - 256 OR currentTick + 256).<br><br><code>1</code> = <code>true</code> -> The tick number returned is initialized;<br><code>false</code> -> The tick number returned is uninitialized.</td></tr></tbody></table>

***

### nextInitializedTickWithinFixedDistance() - `public` `static`

Searches for the next initialized tick up to the distance specified.

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tick</td><td>number</td><td>The tick number that functions as the starting point for the search.</td></tr><tr><td>lte</td><td>boolean</td><td><code>true</code> = Searches for the next initialized tick that is less than or equal to the specified tick.<br><code>false</code> = Searches for the next initialized tick that is greater than the specified tick.</td></tr><tr><td>distance</td><td>number</td><td>The distance from the current active tick to search. Default is <code>480</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>[number, boolean]</td><td>An array whose indexes contain the following values:<br><br><code>0</code> = The next initialized tick up to the distance specified from current active tick. If the next initialized tick is not within the distance specified, the value returned will be the last uninitialized tick from the current active tick (currentTick - distance OR currentTick + distance).<br><br><code>1</code> = <code>true</code> -> The tick number returned is initialized;<br><code>false</code> -> The tick number returned is uninitialized.</td></tr></tbody></table>
