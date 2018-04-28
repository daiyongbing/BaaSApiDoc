BaaS API使用说明
===================

2.1 简介
+++++++++++++
享链云区块链致力于为企业提供金融级别区块链基础设施服务，通过区块链云上的服务，为行业提供安全、可靠、灵活的解决方案。打造一个开放分享、能力全面，标准统一的区块链生态圈，
为众多行业客户提供完备的区块链服务。

2.1.1 API 快速入门
---------------------
	
	API分为交易查询和交易发起两大类。
	
	**“交易查询”接口：** 查询对象的属性值，例如区块信息、交易信息、证书信息等。查询操作不会更改账本状态。
	
	**“交易发起”接口：** 交易的发起包含deploy和invoke两种操作，涉及对账本属性的查询或更改。


2.2 API 概览
++++++++++++++

	**交易相关接口**
	
	.. image:: ./images/howtouse/API_TABLE.jpg
	   :height: 837
	   :width: 1464
	   :scale: 50
	   :alt: API概览

2.3 交易相关接口
++++++++++++++++++++

2.3.1 查询接口
------------------

	**1. 启动系统**
	
	**接口描述**
	
	本接口用于启动repchain服务

	接口请求域名：http://www.repchain.net.org/system/start/

	*输入参数*
	
	.. image:: ./images/howtouse/startsys.jpg
	   :height: 184
	   :width: 1464
	   :scale: 50
	   :alt: 启动系统
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/startSysResult.jpg
	   :height: 307
	   :width: 1462
	   :scale: 50
	   :alt: 启动系统结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		GET "http://localhost:8081/system/start/5" -H  "accept: application/json"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "result": {
			"status": "success"
		  }
		}


	**2. 停止系统**
	
	**接口描述**
	
	本接口用于停止repchain服务

	接口请求域名：http://www.repchain.net.org/system/stop/

	*输入参数*
	
	.. image:: ./images/howtouse/stopsys.jpg
	   :height: 383
	   :width: 1463
	   :scale: 50
	   :alt: 停止系统系统
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/StopSysResult.jpg
	   :height: 278
	   :width: 1463
	   :scale: 50
	   :alt: 停止系统结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		GET "http://localhost:8081/system/stop/5/6" -H  "accept: application/json"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "result": {
			"status": "success"
		  }
		}
	

	**3. 根据blockId查询区块**
	
	**接口描述**
	
	本接口用于用于查询指定ID的区块详细信息

	接口请求域名：http://www.repchain.net.org/block/hash/

	*输入参数*
	
	.. image:: ./images/howtouse/queryBlockbyId_params.jpg
	   :height: 265
	   :width: 1462
	   :scale: 50
	   :alt: 根据blockId查询区块
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/queryBlockbyId_result.jpg
	   :height: 307
	   :width: 1462
	   :scale: 50
	   :alt: 查询区块结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		GET "http://localhost:8081/block/hash/YWU4YTViODFlMzJkZTc1MDA3YzgyMDA2NjFiNzQyYzQ0NDg5MDgyNzIzNjY1NjZjNDU2MWVhNDUwNTU2Y2E5MQ%3D" -H  "accept: application/json"
	
	
	输出
	
	.. code-block:: json
		:linenos:

		{
		  "result": {
			"version": 1,
			"timestamp": "2018-04-20T10:38:44.441Z",
			"transactions": [
			  {
				"type": "CHAINCODE_INVOKE",
				"chaincodeID": "cGF0aDogInBhdGgiCm5hbWU6ICJhZGRkODNkYTljMDY1YzE5ZTFlMzkyY2Q4ZGNhMGQ1MjY4Mzk4YTExZmNiNjU0ZTVmMWMxYWE3MzFhMGFjMDVjIgo=",
				"payload": {
				  "chaincodeID": {
					"path": "path",
					"name": "addd83da9c065c19e1e392cd8dca0d5268398a11fcb654e5f1c1aa731a0ac05c"
				  },
				  "ctorMsg": {
					"function": "put_proof('cd300ff59c988ef1183c3dbd4318e502706881794249e734146cee51837e3dfb','eyJvd25lcl9hY2NvdW50X2FkZHJlc3MiOiIxTUg5eGVkUFRrV1RoSlVnVDhaWWVoaUdDTTdiRVpUVkdOIiwiaGFzaF9hbGdvcml0aG0iOnsibmFtZSI6InNoYTI1NiIsInBhcmFtZXRlciI6IiJ9LCJwaWN0dXJlX2RpZ2l0YWxfaWRlbnRpdHkiOiJjZDMwMGZmNTljOTg4ZWYxMTgzYzNkYmQ0MzE4ZTUwMjcwNjg4MTc5NDI0OWU3MzQxNDZjZWU1MTgzN2UzZGZiIiwicGljdHVyZV9kZXNjIjp7ImF1dGhvciI6InZpYyIsIm5hbWUiOiLlj6/op4bljJbnlYzpnaIiLCJkZXNjIjoiIiwiZmlsZV90eXBlIjoiaW1hZ2UvcG5nIiwiZmlsZV9zaXplIjoyODgxNH19');"
				  },
				  "timeout": 1000,
				  "secureContext": "secureContext",
				  "codePackage": "c3RyaW5n"
				},
				"metadata": "rO0ABXNyACBzY2FsYS5jb2xsZWN0aW9uLm11dGFibGUuSGFzaE1hcAAAAAAAAAABAwAAeHB3DQAAAu4AAAABAAAABAB0AINjX2FkZGQ4M2RhOWMwNjVjMTllMWUzOTJjZDhkY2EwZDUyNjgzOThhMTFmY2I2NTRlNWYxYzFhYTczMWEwYWMwNWNfY2QzMDBmZjU5Yzk4OGVmMTE4M2MzZGJkNDMxOGU1MDI3MDY4ODE3OTQyNDllNzM0MTQ2Y2VlNTE4MzdlM2RmYnB4",
				"txid": "f1b88720-4443-11e8-b8d5-2de829164969",
				"timestamp": "2018-04-20T02:38:44.370Z",
				"confidentialityLevel": "CONFIDENTIAL",
				"confidentialityProtocolVersion": "confidentialityProtocolVersion-1.0",
				"nonce": "bm9uY2U=",
				"toValidators": "dG9WYWxpZGF0b3Jz",
				"cert": "MU1IOXhlZFBUa1dUaEpVZ1Q4WlllaGlHQ003YkVaVFZHTg==",
				"signature": "MEYCIQCjt0IjQfJbJSOChnLHXAWIqFqN3NYQhGEvRp7O7LzUWQIhAO6pkOjpKeSjDeRADu7MLMsbfrH3n1Tz2kqd3Ei/VfFf"
			  }
			],
			"stateHash": "ODlmYjQzZjk5MDY5YjM3Y2NjMDQyYmFjODEzMmVlYmFjMzJiMzI5NDhhODM3ZjdiNGViZDcwMmEyYzNkYTdmYw==",
			"previousBlockHash": "NzlkYzFjZTc4MTg1NjQxOTEwMGEyNGJlODIwYjc0NTQ3MDEwYjc5ZjdlNTAxNjhlZGU0NWJkNzNhNzI2YmIxNw==",
			"consensusMetadata": [
			  {
				"endorser": "MTJrQXpxcWh1cTd4WWdtOVlUcGgxYjl6bUNwWlB5VVd4Zg==",
				"signature": "MEUCIQC/eZxxdj6gbfNlTkvdgMp7LAurE0dsCG+t9FCvYSS3IgIgBEMNUkhVWPccMd/DHkSL8mP27sT2d2tFVW6lwnA1Wq8="
			  },
			  {
				"endorser": "MUFxWnM2dmhjTGlpVHZGeHFTNUNFcU13NnhXdVg5eHF5aQ==",
				"signature": "MEQCIFn+pip8VjX6oUB2MWfnIsvetfhq9svpNvVKf6Qk4IBIAiAA5yPjzS9lg8aMGx/cJSERuzUlyD8E/QB0xeOEY2p8hw=="
			  },
			  {
				"endorser": "MUd2dkhDRlpQYWpxNXlWWTQ0bjdiZG1TZnYyTUo1THlMcw==",
				"signature": "MEUCIQCMCzktu03gPxBNnkdK1AYlb85oReCcDzZ8beALIQRPCQIgDbNjyJBI9s9D5Hx1JMNAK/g799GNOkPK/zA7xOeXUXw="
			  }
			],
			"nonHashData": {
			  "localLedgerCommitTimestamp": "2018-04-20T10:38:44.455Z",
			  "transactionResults": [
				{
				  "txid": "f1b88720-4443-11e8-b8d5-2de829164969",
				  "ol": [
					{
					  "key": "cd300ff59c988ef1183c3dbd4318e502706881794249e734146cee51837e3dfb",
					  "newValue": "ImV5SnZkMjVsY2w5aFkyTnZkVzUwWDJGa1pISmxjM01pT2lJeFRVZzVlR1ZrVUZSclYxUm9TbFZuVkRoYVdXVm9hVWREVFRkaVJWcFVWa2RPSWl3aWFHRnphRjloYkdkdmNtbDBhRzBpT25zaWJtRnRaU0k2SW5Ob1lUSTFOaUlzSW5CaGNtRnRaWFJsY2lJNklpSjlMQ0p3YVdOMGRYSmxYMlJwWjJsMFlXeGZhV1JsYm5ScGRIa2lPaUpqWkRNd01HWm1OVGxqT1RnNFpXWXhNVGd6WXpOa1ltUTBNekU0WlRVd01qY3dOamc0TVRjNU5ESTBPV1UzTXpReE5EWmpaV1UxTVRnek4yVXpaR1ppSWl3aWNHbGpkSFZ5WlY5a1pYTmpJanA3SW1GMWRHaHZjaUk2SW5acFl5SXNJbTVoYldVaU9pTGxqNi9vcDRibGpKYm5sWXpwbmFJaUxDSmtaWE5qSWpvaUlpd2labWxzWlY5MGVYQmxJam9pYVcxaFoyVXZjRzVuSWl3aVptbHNaVjl6YVhwbElqb3lPRGd4TkgxOSI="
					}
				  ]
				}
			  ]
			}
		  }
		}
		
	**4. 查询指定高度的区块**
	
	**接口描述**
	
	本接口用于用于查询指定高度的区块详细信息

	接口请求域名：http://www.repchain.net.org/block/

	*输入参数*
	
	.. image:: ./images/howtouse/queryBlockbyHeight_params.jpg
	   :height: 260
	   :width: 1464
	   :scale: 50
	   :alt: 查询指定高度的区块
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/queryBlockbyHeight_result.jpg
	   :height: 307
	   :width: 1462
	   :scale: 50
	   :alt: 查询指定高度的区块结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		GET "http://localhost:8081/block/15052" -H  "accept: application/json"

	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "result": {
			"version": 1,
			"timestamp": "2018-04-20T10:38:44.441Z",
			"transactions": [
			  {
				"type": "CHAINCODE_INVOKE",
				"chaincodeID": "cGF0aDogInBhdGgiCm5hbWU6ICJhZGRkODNkYTljMDY1YzE5ZTFlMzkyY2Q4ZGNhMGQ1MjY4Mzk4YTExZmNiNjU0ZTVmMWMxYWE3MzFhMGFjMDVjIgo=",
				"payload": {
				  "chaincodeID": {
					"path": "path",
					"name": "addd83da9c065c19e1e392cd8dca0d5268398a11fcb654e5f1c1aa731a0ac05c"
				  },
				  "ctorMsg": {
					"function": "put_proof('cd300ff59c988ef1183c3dbd4318e502706881794249e734146cee51837e3dfb','eyJvd25lcl9hY2NvdW50X2FkZHJlc3MiOiIxTUg5eGVkUFRrV1RoSlVnVDhaWWVoaUdDTTdiRVpUVkdOIiwiaGFzaF9hbGdvcml0aG0iOnsibmFtZSI6InNoYTI1NiIsInBhcmFtZXRlciI6IiJ9LCJwaWN0dXJlX2RpZ2l0YWxfaWRlbnRpdHkiOiJjZDMwMGZmNTljOTg4ZWYxMTgzYzNkYmQ0MzE4ZTUwMjcwNjg4MTc5NDI0OWU3MzQxNDZjZWU1MTgzN2UzZGZiIiwicGljdHVyZV9kZXNjIjp7ImF1dGhvciI6InZpYyIsIm5hbWUiOiLlj6/op4bljJbnlYzpnaIiLCJkZXNjIjoiIiwiZmlsZV90eXBlIjoiaW1hZ2UvcG5nIiwiZmlsZV9zaXplIjoyODgxNH19');"
				  },
				  "timeout": 1000,
				  "secureContext": "secureContext",
				  "codePackage": "c3RyaW5n"
				},
				"metadata": "rO0ABXNyACBzY2FsYS5jb2xsZWN0aW9uLm11dGFibGUuSGFzaE1hcAAAAAAAAAABAwAAeHB3DQAAAu4AAAABAAAABAB0AINjX2FkZGQ4M2RhOWMwNjVjMTllMWUzOTJjZDhkY2EwZDUyNjgzOThhMTFmY2I2NTRlNWYxYzFhYTczMWEwYWMwNWNfY2QzMDBmZjU5Yzk4OGVmMTE4M2MzZGJkNDMxOGU1MDI3MDY4ODE3OTQyNDllNzM0MTQ2Y2VlNTE4MzdlM2RmYnB4",
				"txid": "f1b88720-4443-11e8-b8d5-2de829164969",
				"timestamp": "2018-04-20T02:38:44.370Z",
				"confidentialityLevel": "CONFIDENTIAL",
				"confidentialityProtocolVersion": "confidentialityProtocolVersion-1.0",
				"nonce": "bm9uY2U=",
				"toValidators": "dG9WYWxpZGF0b3Jz",
				"cert": "MU1IOXhlZFBUa1dUaEpVZ1Q4WlllaGlHQ003YkVaVFZHTg==",
				"signature": "MEYCIQCjt0IjQfJbJSOChnLHXAWIqFqN3NYQhGEvRp7O7LzUWQIhAO6pkOjpKeSjDeRADu7MLMsbfrH3n1Tz2kqd3Ei/VfFf"
			  }
			],
			"stateHash": "ODlmYjQzZjk5MDY5YjM3Y2NjMDQyYmFjODEzMmVlYmFjMzJiMzI5NDhhODM3ZjdiNGViZDcwMmEyYzNkYTdmYw==",
			"previousBlockHash": "NzlkYzFjZTc4MTg1NjQxOTEwMGEyNGJlODIwYjc0NTQ3MDEwYjc5ZjdlNTAxNjhlZGU0NWJkNzNhNzI2YmIxNw==",
			"consensusMetadata": [
			  {
				"endorser": "MTJrQXpxcWh1cTd4WWdtOVlUcGgxYjl6bUNwWlB5VVd4Zg==",
				"signature": "MEUCIQC/eZxxdj6gbfNlTkvdgMp7LAurE0dsCG+t9FCvYSS3IgIgBEMNUkhVWPccMd/DHkSL8mP27sT2d2tFVW6lwnA1Wq8="
			  },
			  {
				"endorser": "MUFxWnM2dmhjTGlpVHZGeHFTNUNFcU13NnhXdVg5eHF5aQ==",
				"signature": "MEQCIFn+pip8VjX6oUB2MWfnIsvetfhq9svpNvVKf6Qk4IBIAiAA5yPjzS9lg8aMGx/cJSERuzUlyD8E/QB0xeOEY2p8hw=="
			  },
			  {
				"endorser": "MUd2dkhDRlpQYWpxNXlWWTQ0bjdiZG1TZnYyTUo1THlMcw==",
				"signature": "MEUCIQCMCzktu03gPxBNnkdK1AYlb85oReCcDzZ8beALIQRPCQIgDbNjyJBI9s9D5Hx1JMNAK/g799GNOkPK/zA7xOeXUXw="
			  }
			],
			"nonHashData": {
			  "localLedgerCommitTimestamp": "2018-04-20T10:38:44.455Z",
			  "transactionResults": [
				{
				  "txid": "f1b88720-4443-11e8-b8d5-2de829164969",
				  "ol": [
					{
					  "key": "cd300ff59c988ef1183c3dbd4318e502706881794249e734146cee51837e3dfb",
					  "newValue": "ImV5SnZkMjVsY2w5aFkyTnZkVzUwWDJGa1pISmxjM01pT2lJeFRVZzVlR1ZrVUZSclYxUm9TbFZuVkRoYVdXVm9hVWREVFRkaVJWcFVWa2RPSWl3aWFHRnphRjloYkdkdmNtbDBhRzBpT25zaWJtRnRaU0k2SW5Ob1lUSTFOaUlzSW5CaGNtRnRaWFJsY2lJNklpSjlMQ0p3YVdOMGRYSmxYMlJwWjJsMFlXeGZhV1JsYm5ScGRIa2lPaUpqWkRNd01HWm1OVGxqT1RnNFpXWXhNVGd6WXpOa1ltUTBNekU0WlRVd01qY3dOamc0TVRjNU5ESTBPV1UzTXpReE5EWmpaV1UxTVRnek4yVXpaR1ppSWl3aWNHbGpkSFZ5WlY5a1pYTmpJanA3SW1GMWRHaHZjaUk2SW5acFl5SXNJbTVoYldVaU9pTGxqNi9vcDRibGpKYm5sWXpwbmFJaUxDSmtaWE5qSWpvaUlpd2labWxzWlY5MGVYQmxJam9pYVcxaFoyVXZjRzVuSWl3aVptbHNaVjl6YVhwbElqb3lPRGd4TkgxOSI="
					}
				  ]
				}
			  ]
			}
		  }
		}

	**5. 查询当前块链信息**
	
	**接口描述**
	
	本接口用于用于查询指定ID的区块详细信息

	接口请求域名：http://www.repchain.net.org/chaininfo

	*输入参数*
	
	无输入参数
	   
	**输出参数**
	
	.. image:: ./images/howtouse/chaininfo_result.jpg
	   :height: 780
	   :width: 1465
	   :scale: 50
	   :alt: 查询当前块链信息结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		GET "http://localhost:8081/chaininfo" -H  "accept: application/json"
	
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "result": {
			"height": "15052",
			"totalTransactions": "150477",
			"currentBlockHash": "YWU4YTViODFlMzJkZTc1MDA3YzgyMDA2NjFiNzQyYzQ0NDg5MDgyNzIzNjY1NjZjNDU2MWVhNDUwNTU2Y2E5MQ==",
			"previousBlockHash": "NzlkYzFjZTc4MTg1NjQxOTEwMGEyNGJlODIwYjc0NTQ3MDEwYjc5ZjdlNTAxNjhlZGU0NWJkNzNhNzI2YmIxNw==",
			"currentWorldStateHash": "ODlmYjQzZjk5MDY5YjM3Y2NjMDQyYmFjODEzMmVlYmFjMzJiMzI5NDhhODM3ZjdiNGViZDcwMmEyYzNkYTdmYw=="
		  }
		}

	**6. 根据transactionId查询交易**
	
	**接口描述**
	
	本接口用于用于查询指定ID的区块详细信息

	接口请求域名：http://www.repchain.net.org/transaction/

	*输入参数*
	
	.. image:: ./images/howtouse/queryTrans_params.jpg
	   :height: 266
	   :width: 1462
	   :scale: 50
	   :alt: 根据transactionId查询交易
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/queryTrans_result.jpg
	   :height: 307
	   :width: 1462
	   :scale: 50
	   :alt: 交易查询结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		GET "http://localhost:8081/transaction/f1b88720-4443-11e8-b8d5-2de829164969" -H  "accept: application/json"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "result": {
			"type": "CHAINCODE_INVOKE",
			"chaincodeID": "cGF0aDogInBhdGgiCm5hbWU6ICJhZGRkODNkYTljMDY1YzE5ZTFlMzkyY2Q4ZGNhMGQ1MjY4Mzk4YTExZmNiNjU0ZTVmMWMxYWE3MzFhMGFjMDVjIgo=",
			"payload": {
			  "chaincodeID": {
				"path": "path",
				"name": "addd83da9c065c19e1e392cd8dca0d5268398a11fcb654e5f1c1aa731a0ac05c"
			  },
			  "ctorMsg": {
				"function": "put_proof('cd300ff59c988ef1183c3dbd4318e502706881794249e734146cee51837e3dfb','eyJvd25lcl9hY2NvdW50X2FkZHJlc3MiOiIxTUg5eGVkUFRrV1RoSlVnVDhaWWVoaUdDTTdiRVpUVkdOIiwiaGFzaF9hbGdvcml0aG0iOnsibmFtZSI6InNoYTI1NiIsInBhcmFtZXRlciI6IiJ9LCJwaWN0dXJlX2RpZ2l0YWxfaWRlbnRpdHkiOiJjZDMwMGZmNTljOTg4ZWYxMTgzYzNkYmQ0MzE4ZTUwMjcwNjg4MTc5NDI0OWU3MzQxNDZjZWU1MTgzN2UzZGZiIiwicGljdHVyZV9kZXNjIjp7ImF1dGhvciI6InZpYyIsIm5hbWUiOiLlj6/op4bljJbnlYzpnaIiLCJkZXNjIjoiIiwiZmlsZV90eXBlIjoiaW1hZ2UvcG5nIiwiZmlsZV9zaXplIjoyODgxNH19');"
			  },
			  "timeout": 1000,
			  "secureContext": "secureContext",
			  "codePackage": "c3RyaW5n"
			},
			"metadata": "rO0ABXNyACBzY2FsYS5jb2xsZWN0aW9uLm11dGFibGUuSGFzaE1hcAAAAAAAAAABAwAAeHB3DQAAAu4AAAABAAAABAB0AINjX2FkZGQ4M2RhOWMwNjVjMTllMWUzOTJjZDhkY2EwZDUyNjgzOThhMTFmY2I2NTRlNWYxYzFhYTczMWEwYWMwNWNfY2QzMDBmZjU5Yzk4OGVmMTE4M2MzZGJkNDMxOGU1MDI3MDY4ODE3OTQyNDllNzM0MTQ2Y2VlNTE4MzdlM2RmYnB4",
			"txid": "f1b88720-4443-11e8-b8d5-2de829164969",
			"timestamp": "2018-04-20T02:38:44.370Z",
			"confidentialityLevel": "CONFIDENTIAL",
			"confidentialityProtocolVersion": "confidentialityProtocolVersion-1.0",
			"nonce": "bm9uY2U=",
			"toValidators": "dG9WYWxpZGF0b3Jz",
			"cert": "MU1IOXhlZFBUa1dUaEpVZ1Q4WlllaGlHQ003YkVaVFZHTg==",
			"signature": "MEYCIQCjt0IjQfJbJSOChnLHXAWIqFqN3NYQhGEvRp7O7LzUWQIhAO6pkOjpKeSjDeRADu7MLMsbfrH3n1Tz2kqd3Ei/VfFf"
		  }
		}
		
	**7. 查询证书短地址**
	
	**接口描述**
	
	本接口用于用于查询指定ID的区块详细信息

	接口请求域名：http://www.repchain.net.org/certAddr/getAddrByCert

	*输入参数*
	
	.. image:: ./images/howtouse/getaddrbycert_params.jpg
	   :height: 363
	   :width: 1461
	   :scale: 50
	   :alt: 查询证书短地址
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/getaddrbycert_result.jpg
	   :height: 492
	   :width: 1462
	   :scale: 50
	   :alt: 查询证书短地址结果
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
		
		POST "http://localhost:8081/certAddr/getAddrByCert" -H  "accept: application/json" -H  "content-type: application/json" -d \
		"{  \"cert\": \"LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJtakNDQVQrZ0F3SUJBZ0lFV1dWK0F6QUtCZ2dxaGtqT1BRUURBakJXTVFzd0NRWURWUVFHRXdKamJqRUxNQWtHQTFVRUNBd0NZbW94Q3pBSkJnTlZCQWNNQW \
		1KcU1SRXdEd1lEVlFRS0RBaHlaWEJqYUdGcGJqRU9NQXdHQTFVRUN3d0ZhWE5qWVhNeENqQUlCZ05WQkFNTUFURXdIaGNOTVRjd056RXlNREUwTWpFMVdoY05NVGd3TnpFeU1ERTBNakUxV2pCV01Rc3dDUVlEVlFRR0V3SmpiakVMTUFrR0 \
		ExVUVDQXdDWW1veEN6QUpCZ05WQkFjTUFtSnFNUkV3RHdZRFZRUUtEQWh5WlhCamFHRnBiakVPTUF3R0ExVUVDd3dGYVhOallYTXhDakFJQmdOVkJBTU1BVEV3VmpBUUJnY3Foa2pPUFFJQkJnVXJnUVFBQ2dOQ0FBVDZWTEUvZUY5K3NLMVJ \
		PbjhuNng3aEtzQnhlaFc0MnFmMUlCOHF1Qm41T3JRRDN4Mkg0eVpWRHdQZ2NFVUNqSDhQY0Znc3dkdGJvOEpMLzdmNjZ5RUNNQW9HQ0NxR1NNNDlCQU1DQTBrQU1FWUNJUUN1ZCs0LzNuam5mVWtHOWZmU3FjSGhuc3VaTk1Rd2FXNjJFVlhi \
		Y2pvaUJnSWhBUG9MSksxRDA2SU1vaG9sWWNzZ1RRYjVUcnJlai9lclpPTk1tMWNTMWlQKwotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0t\",  \"cid\": \"string\"}"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "addr": "1MH9xedPTkWThJUgT8ZYehiGCM7bEZTVGN",
		  "err": ""
		}
		
	**8. 根据证书短地址查询证书字符串**
	
	**接口描述**
	
	本接口用于用于查询指定ID的区块详细信息

	接口请求域名：http://www.repchain.net.org/certAddr/getCertByAddr

	*输入参数*
	
	.. image:: ./images/howtouse/getcertbyaddr_params.jpg
	   :height: 367
	   :width: 1465
	   :scale: 50
	   :alt: 根据证书短地址查询证书字符串
	   
	   
	**输出参数**
	
	.. image:: ./images/howtouse/getcertbyaddr_result.jpg
	   :height: 704
	   :width: 1462
	   :scale: 50
	   :alt: 根据证书短地址查询证书字符串
	   
	**示例**
	
	输入
	
	.. code-block:: shell
		:linenos:
	
		POST "http://localhost:8081/certAddr/getCertByAddr" -H  "accept: application/json" -H  "content-type: application/json" -d \
		"{  \"addr\": \"string\",  \"cid\": \"addd83da9c065c19e1e392cd8dca0d5268398a11fcb654e5f1c1aa731a0ac05c\"}"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "addr": "string",
		  "cert": "",
		  "cid": "addd83da9c065c19e1e392cd8dca0d5268398a11fcb654e5f1c1aa731a0ac05c",
		  "err": "不存在证书"
		}
		


2.3.2 交易发起
-----------------

	**1. deploy**
	
	**接口描述**
	
	本接口（deploy）用于部署链码，其将Shim接口中的方法部署到Sandbox中隔离运行，供invoke调用。

	接口请求域名：http://www.repchain.net.org/transaction/

	输入参数
	
	.. image:: ./images/howtouse/deploy_paras.jpg
	   :height: 743
	   :width: 1462
	   :scale: 50
	   :alt: deploy交易
	   
	输出参数
	
	.. image:: ./images/howtouse/deploy_result.jpg
	   :height: 743
	   :width: 1462
	   :scale: 50
	   :alt: deploy交易结果
	   
	   
	**示例**
	
	输入

	.. code-block:: shell
		:linenos:
		
		POST "http://localhost:8081/transaction/postTran" -H  "accept: application/json" -H  "content-type: application/json" -d \
		"{  \"stype\": 1,  \"idPath\": \"\",  \"iptFunc\": \"\",  \"iptArgs\": [],  \"timeout\": 0,  \"secureContext\": \"string\",  \"code\": \" \
		function write(pm){for(x in pm){shim.setVal(x,pm[x]);}} function read(pn){return shim.getVal(pn);}\"  \"ctype\": 0}"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "txid": "9354e6c8a5e1b73ce319b6afd29bbc1f54b4ed064c785b9d3f913ea90e0fb23c",
		  "result": "9354e6c8a5e1b73ce319b6afd29bbc1f54b4ed064c785b9d3f913ea90e0fb23c",
		  "ol": [
			{
			  "key": "c_9354e6c8a5e1b73ce319b6afd29bbc1f54b4ed064c785b9d3f913ea90e0fb23c",
			  "oldValue": null,
			  "newValue": [
				57, 51, 53, 52, 101, 54, 99, 56, 97, 53, 101, 49, 98, 55, 51,
				99, 101, 51, 49, 57, 98, 54, 97, 102, 100, 50, 57, 98, 98, 99,
				49, 102, 53, 52, 98, 52, 101, 100, 48, 54, 52, 99, 55, 56, 53,
				98, 57, 100, 51, 102, 57, 49, 51, 101, 97, 57, 48, 101, 48, 102,
				98, 50, 51, 99 ]
			}
		  ]
		}
	

	**2. invoke**
	
	**接口描述**
	
	本接口（deploy）用于调用链码，其将调用deploy中部署的方法对账本状态查询或更改。

	接口请求域名：http://www.repchain.net.org/transaction/

	输入参数
	
	.. image:: ./images/howtouse/invoke_params.jpg
	   :height: 743
	   :width: 1462
	   :scale: 50
	   :alt: deploy交易
	   
	输出参数
	
	.. image:: ./images/howtouse/invoke_result.jpg
	   :height: 743
	   :width: 1462
	   :scale: 50
	   :alt: deploy交易
	   
	**示例**
	
	输入

	.. code-block:: shell
		:linenos:
		
		POST "http://localhost:8081/transaction/postTran" -H  "accept: application/json" -H  "content-type: application/json" -d " \
		{  \"stype\": 2,  \"idPath\": \"\",  \"idName\": \"9354e6c8a5e1b73ce319b6afd29bbc1f54b4ed064c785b9d3f913ea90e0fb23c\",  \"iptFunc\": \"write({'test1':10000}); \
		read('test1');\",  \"iptArgs\": [],  \"timeout\": 0,  \"secureContext\": \"string\",  \"code\": \"string\"  \"ctype\": 0}"
	
	输出
	
	.. code-block:: json
		:linenos:
		
		{
		  "txid": "ef3388a0-0637-11e8-bc31-0f000027000a",
		  "result": 10000,
		  "ol": [
			{
			  "key": "test1",
			  "oldValue": [49, 48, 48, 48],
			  "newValue": [49, 48, 48, 48, 48]
			}
		  ]
		}

2.4 错误码
++++++++++++

	.. image:: ./images/howtouse/errCode.jpg
	   :height: 524
	   :width: 1462
	   :scale: 50
	   :alt: 错误码


