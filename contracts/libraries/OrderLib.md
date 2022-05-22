#### Features

This library contains struct `OrderData` with some functions for this struct:
- hash: calculates hash according to EIP-712 rules. you can find type definitions
- hashKey: calculates key for Order used to record fill of the order (orders with the same key considered as an update)
- validate: validates main order parameters, checks if `OrderData` can be processed

`OrderData` fields:
- `address` maker
- `AssetData` makerAsset
- `address` taker (can be zero address)
- `AssetData` takerAsset
- `uint` salt - random number to distinguish different maker's Orders
- `uint` start - Order can't be matched before this date (optional)
- `uint` end - Order can't be matched after this date (optional)
- `bytes4` orderType - type of order, usually hash of some string, e.g.: "CREATE_ORDER_TYPE", "UPDATE_ORDER_TYPE"
- `bytes` data - generic data, can be anything, extendable part of the order

#### Types for EIP-712 signature:
```javascript
const Types = {
	AssetType: [
		{name: 'assetClass', type: 'bytes4'},
		{name: 'data', type: 'bytes'}
	],
	AssetData: [
		{name: 'assetType', type: 'AssetType'},
		{name: 'value', type: 'uint256'}
	],
	OrderData: [
		{name: 'maker', type: 'address'},
		{name: 'makeAsset', type: 'AssetData'},
		{name: 'taker', type: 'address'},
		{name: 'takeAsset', type: 'AssetData'},
		{name: 'forwarder', type: 'address'},
		{name: 'salt', type: 'uint256'},
		{name: 'start', type: 'uint256'},
		{name: 'end', type: 'uint256'},
		{name: 'orderType', type: 'bytes4'},
		{name: 'data', type: 'bytes'},
	]
};
```
