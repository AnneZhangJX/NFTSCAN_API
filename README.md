# NFTSCAN
# NFTSCAN开发API
##接口描述 

NFTSCAN对外开发NFT资产信息查询说明，一共有两个接口，第一个接口查询NFTSCAN当前收集的所有的合约项目，包含合约地址和项目基本信息。
第二个接口可以通过合约地址查询某个项目下的所有NFT资产详细信息。

http://api.nftscan.com/nftmsg/

## 查询NFTSCAN已收录的NFT项目

请求链接

nftproject/all

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| page_size | String | 每一页返回数据条数 |
| page_index | String | 页数 |

返回参数

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| status | int | 返回状态 |
| code | int | 状态码 |
| time | String | 时间 |
| message | String | 消息 |
| nft_platform_num | int | NFT项目总数 |
| nft_platform_list | List | NFT项目列表 |


### nft_platform_list
| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| nft_platform_name | String | NFT项目名称 |
| nft_platform_time | String | NFT项目发起时间 |
| nft_platform_type | String | NFT项目类型 （1155/721）|
| nft_platform_contract | String | NFT项目合约地址 |
| nft_platform_describe | String | NFT项目简介 |
| nft_metadata_status | int | 元数据保存状态(ipfs/其他) |
| nft_is_ipfs | int | 是否从IPFS二次获取元数据 （是，否）|
| nft_ipfs_svae | int | IPFS是否查询数据并进行保存（已保存，未保存，部分保存） |


数据示例

```json
{
    "status":0,
    "code":2001,
    "time":"2020-11-14 16:25:22",
    "message":"请求次数超过限制",
    "nft_platform_num":2,
    "nft_platform_list":[
        {
            "nft_platform_name":"UNI",
            "nft_platform_type":"1155/721",
            "nft_platform_time":"2381832894",
            "nft_platform_contract":"0xc83e009c7794e8f6d1954dc13c23a35fc4d039f6",
            "nft_platform_describe":"UNI is .....",
             "nft_platform_contract":"0xc83e009c7794e8f6d1954dc13c23a35fc4d039f6",
             "nft_metadata_status":"1",
             "nft_is_ipfs":"1",
             "nft_ipfs_svae":"0",
        }
    ]
}
```





## 根据合约地址查询NFT项目下所有资产信息

请求参数

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| nft_address | String | NFT合约地址 |
| page_size | String | 每一页返回数据条数 |
| page_index | String | 页数 |

nft/total_message/nft_address

返回参数

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| status | int | 返回状态 |
| code | int | 状态码 |
| time | String | 时间 |
| message | String | 消息 |
| nft_message_List | Object | NFT详细信息列表，时间近到远 |

nft_message_List

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| nft_asset_id | String | NFT资产ID |
| nft_creator | String | NFT铸造发起地址 |
| nft_holder | String | NFT资产当前持有者 |
| nft_create_time | String | NFT铸造时间 |
| nft_creat_hash | String | NFT铸造hash |
| nft_content_uri | String | NFT元数据链接 |
| nft_detail | String | NFT详情 |


数据示例

```json
{
    "status":0,
    "code":2001,
    "time":"2020-11-14 16:25:22",
    "message":"请求次数超过限制",
    "nft_message_List":[
        {
            "nft_asset_id":11254725,
            "nft_creator":"0xc83e009c7794e8f6d1954dc13c23a35fc4d039f6",
            "nft_holder":"0xc83e009c7794e8f6d1954dc13c23a35fc4d039f6",
            "nft_create_time":1628601074,
            "nft_creat_hash":"0xcd6025bdedd26b8cae645348389158b805ee4341369e0c3c84d129ccbe529eac",
            "nft_content_uri":"https://lh3.googleusercontent.com/ECp1wSceVbzN9XBhO4wkse7AwccKoN6ecXVuWwsM4t3m8kNxeYDGLPzIKq3LHxTFxazJYnBGJxhY5vc3_s4ss3Eupg9RPTiGFf93-A",
            "nft_detail":"{\"image\":\"ipfs://QmNQdLr39xXRpr6XghhAD1fd1dntJouugvFhYqQVebMUku\"}"
        }
    ]
}
```


## 更改NFT资产信息在IPFS保存状态

请求参数

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| nft_address | String | NFT合约地址 |
| nft_ipfs_svae | int | IPFS是否查询数据并进行保存（0未保存,1已保存，2部分保存） |

nft/update_ipfs_save_status

返回参数

| 参数名称 | 类型 | 描述 |
| :-----:| :----: | :----: |
| status | int | 返回状态 |
| code | int | 状态码 |
| time | String | 时间 |
| message | String | 消息 |


数据示例

```json
{
    "nft_address":"0xc83e009c7794e8f6d1954dc13c23a35fc4d039f6",
    "nft_ipfs_svae":1
}
```

