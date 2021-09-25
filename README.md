# NFTSCAN
# NFTSCAN开发API NFTSCAN DEVELOP API
##接口描述 interface description

NFTSCAN对外开放NFT资产信息查询说明: (The instruction that NFTSCAN is open NFT asset information query to public)   
接口可查询NFTSCAN当前收集的所有的合约项目，包含合约地址、metadata、tokenuri等信息，可以通过合约地址查询某个项目下的所有NFT资产详细信息。(the interface is able to query all contracts that NFTSCAN has collected including contracts addresses, metadata, tokenuri,etc. And it also can query all NFT assets information in detail of a project by contract address)

IPFS查询NFT资产信息进行保存以后，需要提供一个接口能够通过合约地址+资产ID查询出对应的IPFS存储链接。由于NFT数据不规范性，部分项目的metadata未能查询成功，需要持续补充，nft_metadata_get字段为正常的项目可以批量查询进行保存，异常的需要等nftscan补充metadata。(After IPFS queried NFT assets information and saved, need to provide an interface which can check out the corresponding IPFS storage link by contract address + asset ID. Cause the substandard of NFT date, some projects's metadate are still in query and need continuous supplement. If the nft_metadata_get field shows normal, IPFS can batch search and saving, otherwise, need to wait NFTSCAN supple metadata.

http://api.nftscan.com/nftmsg/

## 查询NFTSCAN已收录的NFT项目( query all NFT projects that NFTSCAN has collected)

请求链接 Request Links

nftproject/all

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| page_size | String | 每一页返回数据条数(counts date response per page) |
| page_index | String | 页数（Number of pages） |

返回参数(response param)

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| status | int | 返回状态（response status) |
| code | int | 状态码(status code) |
| time | String | 时间 (time) |
| message | String | 消息(message) |
| nft_platform_num | int | NFT项目总数(total number of NFT projects |
| nft_platform_list | List | NFT项目列表(NFT projects list) |


### nft_platform_list
| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| nft_platform_name | String | NFT项目名称(NFT project name) |
| nft_platform_time | String | NFT项目发起时间(NFT project launch time) |
| nft_platform_type | String | NFT项目类型 （1155/721）|
| nft_platform_contract | String | NFT项目合约地址(NFT projest contract addresses) |
| nft_platform_describe | String | NFT项目简介(NFT project introduction) |
| nft_metadata_get | int | 元数据获取状态(正常/异常)Metadata acquisition status (normal/abnormal), Skip abnormal metadate, 元数据异常的可以先跳过不保存，NFTSCAN进行数据补充以后，会更改这个状态 NFTSCAN will supplement later and change the status.|
| nft_metadata_status | int | 元数据保存源(ipfs/其他) ，已经保存在IPFS的数据，不需要再保存一次Metadata saving source (ipfs/other), data already saved in IPFS, no need to save it again|
| nft_is_ipfs | int | 是否从IPFS二次获取元数据 （是，否）Whether to obtain metadata from IPFS twice (Yes, No))|
| nft_ipfs_svae | int | IPFS是否查询数据并进行保存（已保存，未保存，部分保存）Whether IPFS queries the data and saves it (saved, unsaved, partially saved)，这个字段需要IPFS方在保存某个项目的数据后调用NFTSCAN的接口更新状态This field requires IPFS to use the NFTSCAN interface to update the status after saving the data of a project|


数据示例Data example

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





## 根据合约地址查询NFT项目下所有资产信息 query all NFT assets information in detail of a project by contract address

请求参数 request param

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| nft_address | String | NFT合约地址 NFT contract address |
| page_size | String | 每一页返回数据条数 counts date response per page |
| page_index | String | 页数 Number of pages|

nft/total_message/nft_address

返回参数 response param

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| status | int | 返回状态 response status |
| code | int | 状态码 status code |
| time | String | 时间 time |
| message | String | 消息 message |
| nft_message_List | Object | NFT详细信息列表，时间近到远 NFT details list, time near to far|

nft_message_List

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| nft_asset_id | String | NFT资产ID (NFT asset ID) |
| nft_creator | String | NFT铸造发起地址 (NFT mint address) |
| nft_holder | String | NFT资产当前持有者( NFT asset holder) |
| nft_create_time | String | NFT铸造时间( NFT mint time) |
| nft_creat_hash | String | NFT铸造hash (NFT mint hash) |
| nft_content_uri | String | NFT TokenUri |
| nft_metadata| String | NFT元数据 (NFT metadate) |


数据示例 Data example

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
            "nft_metadata":"{\"image\":\"ipfs://QmNQdLr39xXRpr6XghhAD1fd1dntJouugvFhYqQVebMUku\"}"
        }
    ]
}
```


## 更新NFT资产信息在IPFS的保存状态 （Update the status of NFT asset information saved in IPFS)
当IPFS方存储完某个项目的NFT资产以后，需要调用这个接口更新保存状态，NFTSCAN会根据这个状态去查询在IPFS中的存储链接。(When IPFS has finished the store of a project and it's NFT assets, it needs to use this interface to update the preservation status, and NFTSCAN will query the storage link in IPFS based on this status)

请求参数(request param)

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| nft_address | String | NFT合约地址(NFT contract address) |
| nft_ipfs_svae | int | IPFS是否查询数据并进行保存（0未保存,1已保存，2部分保存）Whether IPFS queried data and saved(0 unsaved,1 saved, 2 partially saved) |

nft/update_ipfs_save_status

返回参数( response param)

| 参数名称param | 类型type | 描述description |
| :-----:| :----: | :----: |
| status | int | 返回状态 response status |
| code | int | 状态码status code |
| time | String | 时间 time |
| message | String | 消息 message |


数据示例 Data example

```json
{
    "nft_address":"0xc83e009c7794e8f6d1954dc13c23a35fc4d039f6",
    "nft_ipfs_svae":1
}
```

