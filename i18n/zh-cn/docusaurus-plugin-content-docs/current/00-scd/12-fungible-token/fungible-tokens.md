---
title: Fungible tokens
sidebar_position: 1
slug: /fungible-token/fungible-tokens
hide_table_of_contents: true
---

在本课中，我们将探讨同质化代币（Fungible Tokens）及其运作原理。

同质化代币是数字智能合约，提供了与法定货币相同的价值和可交换性。

它们使用户能够在帐户之间交易具有相同价值的代币化资产。在技术上，智能合约通过存储将帐户地址映射到代币数量的方式来实现同质化代币。

同质化代币提供了与法定货币相同的价值和可交换性。

就像将一张纸币兑换成另一张纸币一样，这些数字智能合约允许用户在帐户之间交易具有相同价值的代币化资产。

然而，在基本的技术层面上，同质化代币只是存储帐户地址与代币数量之间的映射的智能合约。

$$
地址 → 数量
$$

这些智能合约的核心功能包括：

- `transfer(from, to, amount)`：此函数允许你从一个地址（`from`）向另一个地址（`to`）转移代币的数量（`amount`）。它会检查 `from` 帐户是否拥有代币，从其余额中减去所需的`amount`并将指定数量的代币添加到 `to` 帐户。
- `approve(spender, amount)`：允许指定的支出者帐户从调用帐户（`msg::source()`）转移代币。通过调用 `transfer()` 函数，支出者帐户可以将代币从 `msg::source()` 帐户移动到指定的地址。这个功能对于合约内部需要的代币转移具有价值。

让我们以托管智能合约为例。

在这里，作为商品的支付，我们使用的是代币，而不是 `msg::value()`。买家发送一个 `deposit()` 消息，促使托管智能合约与代币合约互动并启动代币转移消息。

值得注意的是，此消息中的发件人地址对应于买家。

如果托管合约没有处置买家的代币的权限，代币合约将引发错误并阻止代币转移。

- `mint(to, amount)` - 此函数增加了合约中的代币数量。只有具有权限的特定帐户才能调用此函数来创建新的代币。
- `burn(from, amount)` - 它减少了合约中的代币数量。与 `mint()` 函数类似，只有特定帐户可以使用它来销毁代币。