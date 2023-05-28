# SyncSwap

// 获取 Token 精度信息，如果是NFT，默认返回1
function getTokenDecimal(contractAddress, network) {
  let rpcLink = RPC_MAP[network];
  if (!rpcLink) {
    return "Error: Invalid Network Name";
  }
  const data = '0x313ce567';
  var response = UrlFetchApp.fetch(rpcLink, {
    method: "post",
    payload: JSON.stringify({
      "jsonrpc":"2.0",
      "method":"eth_call",
      "params":[{
        "to": contractAddress,
        "data": data
      }, "latest"],
      "id":1
    }),
    contentType: "application/json",
    muteHttpExceptions: true
  });
