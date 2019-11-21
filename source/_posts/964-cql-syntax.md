---
title: CQL Syntax
tags:
  - Cassandra
  - noSQL
url: 964.html
id: 964
categories:
  - 随笔
date: 2016-04-01 14:11:29
---

This document describes the Cassandra Query Language (CQL) version 3. CQL v3 is not backward compatible with CQL v2 and differs from it in numerous ways. Note that this document describes the last version of the languages. However, the [changes](https://cassandra.apache.org/doc/cql3/CQL.html#changes) section provides the diff between the different versions of CQL v3. CQL v3 offers a model very close to SQL in the sense that data is put in _tables_ containing _rows_ of _columns_. For that reason, when used in this document, these terms (tables, rows and columns) have the same definition than they have in SQL. But please note that as such, they do **not** refer to the concept of rows and columns found in the internal implementation of Cassandra and in the thrift and CQL v2 API. 来源： _[CQL](https://cassandra.apache.org/doc/cql3/CQL.html)_