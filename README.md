# Admixer integration guide.



This document is RTB integration specification for `SSP` which provides inventory real time.  
This document is based on Open RTB version.2.3(Native Ads 1.2).

Therefore, this document does not cover details regarding BidRequest/Response.  
For more details on these, please check OpenRTB 2.3(Native Ads 1.2) specification via below link.

https://www.iab.com/wp-content/uploads/2015/06/OpenRTB-API-Specification-Version-2-3.pdf<br>
https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf

If you have any question about this document, please reach out to admixer@nasmedia.co.kr.  
<br>

# 1. Bid Request Specification
## Object model

Object | Support | OpenRTB 2.3 Section for Reference | Native Ads 1.2 Section for Reference | Extension
:--- | :---: | :---: | :---: | :---
BidRequest | O | 3.2.1 |  | O
Imp | O | 3.2.2 |  | X
Banner | O | 3.2.3 |  | X
Video | O | 3.2.4 |  | X
Native | O | 3.2.5 |  | X
Site | O | 3.2.6 |  | X
App | O | 3.2.7 |  | X
Publisher | X | 3.2.8 |  | -
Content | O | 3.2.9 |  | X
Producer | X | 3.2.10 |  | -
Device | O | 3.2.11 |  | X
Geo | X | 3.2.12 |  | -
User | O | 3.2.13 |  | O
Data | X | 3.2.14 |  | -
Segment | X | 3.2.15 |  | -
Regs | O | 3.2.16 |  | O
PMP | X | 3.2.17 |  | -
Deal | X | 3.2.18 |  | -
Native Markup | O | - | 4.1 | -
Asset | O | - | 4.2 | -
Title | O | - | 4.3 | -
Image | O | - | 4.4 | -
Video | O | - | 4.5 | -
Data | O | - | 4.6 | -
EventTrackers | O | - | 4.7 | -
<br>

## Object Specifications

- Object : BidRequest

Field name | Required
:--- | :---
id | O
imp | O
site | O (at least one among site or app is mandatory)
app | O (at least one among site or app is mandatory)
device | O
user | -
at | - (“Second Price” only)
cur | - (USD only)
bcat | -
badv | -
regs | -
ext | -
<br>

- Object : Imp

Field name | Required
:--- | :---
id | O
banner | O (at least one among banner, video, native is mandatory)
video | O (at least one among banner, video, native is mandatory)
native | O (at least one among banner, video, native is mandatory)
instl | -
bidfloor | -
bidfloorcur | - (USD only)
secure | -
tagid | -
<br>

- Object : Banner

Field name | Required
:--- | :---
w | O
h | O
battr | -
api | -
<br>

- Object : Video

Field name | Required
:--- | :---
mimes | O
minduration | O
maxduration | O
protocols | -
w | -
h | -
skipafter | -
battr | -
api | -
ext | -
<br>

- Object : Native

Field name | Required
:--- | :---
request | O
ver | -
api | -
battr | -
<br>

- Object : Site

Field name | Required
:--- | :---
id | O
name | O
domain | O
cat | O
page | -
publisher | -
content | -
ext | -
<br>

- Object : App

Field name | Required
:--- | :---
id | O
name | O
bundle | O
domain | -
storeurl | O
cat | O
publisher | -
content | -
<br>

- Object : Content

Field name | Required
:--- | :---
id | -
episode | -
series | -
season | -
url | -
cat | -
language | -
<br>

- Object : Device

Field name | Required
:--- | :---
ua | O
geo | -
dnt | -
ip | O (mandatory, public IP)
ipv6 | -
devicetype | O
make | -
model | O
os | O
osv | O
hwv | -
h | -
w | -
ppi | -
pxratio | -
language | O
carrier | O (app only)
connectiontype | -
ifa | O (app only)
<br>

- Object : User

Field name | Required
:--- | :---
id | -
buyerid (buyeruid) | -
ext | -
<br>

- Object : Regs

Field name | Required
:--- | :---
ext | -
<br>


- Object : Native Markup

Field name | Required
:--- | :---
ver | -
context | -
contextsubtype | -
plcmttype | -
plcmtcnt | -
seq | -
assets | O
aurlsupport | -
durlsupport | -
eventtrackers | -
privacy | -
<br>

- Object : Asset

Field name | Required
:--- | :---
Id | O
required | -
title | -
img | -
video | -
data | -
<br>

- Object : Title

Field name | Required
:--- | :---
len | O
<br>

- Object : Image

Field name | Required
:--- | :---
type | -
w | -
wmin | -
h | -
hmin | -
mimes | -
<br>

- Object : Video

Field name | Required
:--- | :---
mimes | O
minduration | O
maxduration | O
protocols | O
<br>

- Object : Data

Field name | Required
:--- | :---
type | O
len | -
<br>

- Object : EventTrackers

Field name | Required
:--- | :---
event | O
methods | O
<br>


## Extentions

- Object : ext of Bidrequest

Field name | Type | Mandatory / Option | Details
:--- | :---: | :---: | :---
clicktrack | int | Option | Macro of click measurement.<br>Where 0 = Not use. In this case, macro of click measurement is not included on Bid.adm of BidResponse (Default value), 1 = Use. In this case, macro of click measurement is included on Bid.adm of BidResponse.
<br>

- Object : ext of Video

Field name | Type | Mandatory / Option | Details
:--- | :---: | :---: | :---
allctvs | int | Option | Whether to request creatives with all resolution.<br>Where 0 = Not use. (Default value), 1 = Use. In this case, all creatives with supported resolutions should be included in the response.
<br>

- Object : ext of Site

Field name | Type | Mandatory / Option | Details
:--- | :---: | :---: | :---
pcweb | int | Option | Whether it is a PC website or not.<br>Where 0 = Mobile website (Default value), 1 = PC website.
<br>

- Object : ext of User

Field name | Type | Mandatory / Option | Details
:--- | :---: | :---: | :---
consent | string | Option | Convey user consent when GDPR regulations are in effect.
<br>

- Object : ext of Regs

Field name | Type | Mandatory / Option | Details
:--- | :---: | :---: | :---
gdpr | int | Mandatory | Whether the user is subject to GDPR or not.<br>Where 0 = No, 1 = Yes.
<br>

## Request sample

## Banner
	{ 
		"id": "0m1hqt5x", 
		"imp": [{ 
			"id": "1", 
			"bidfloor": 0.03, 
			"banner": { 
				"w": 320, 
				"h": 50 
			}}], 
		"app": { 
			"id": "78e87y2f284vry62", 
			"name": "test app", 
			"bundle": "com.app.test", 
			"storeurl": "http://test.test", 
			"cat": ["IAB3"] 
		}, 
		"device": { 
			"ua": "Mozilla/5.0 (Linux; Android 4.4.4; Nexus 5 Build/KTU84P) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/33.0.0.0 Mobile Safari/537.36", 
			"os": "android", 
			"osv": "4.4.4", 
			"model": "SHV-E160K", 
			"ip": "123.145.167.189", 
			"ifa": "f5edbc38-2614-4470-927c-f182fc003411" 
		}, 
		"regs": { 
			"ext": { 
				"gdpr": 0 
			} 
		} 
	}
<br>

## Video
	{ 
		"id": "0m1hqt5x", 
		"imp": [{ 
			"id": "1", 
			"bidfloor": 0.03, 
			"video": { 
				"w": 640, 
				"h": 480, 
				"minduration": 5, 
				"maxduration": 30, 
				"api": [1, 2], 
				"protocols": [2, 3], 
				"mimes": ["video/x-flv", "video/mp4", "application/x-shockwave-flash", "application/javascript"], 
				"battr": [13, 14] 
			} 
		}], 
		"app": { 
			"id": "78e87y2f284vry62", 
			"name": "test app", 
			"bundle": "com.app.test", 
			"storeurl": "http://test.test", 
			"cat": ["IAB3"], 
			"content": { 
				"id": "abcde", 
				"episode": "test episode", 
				"series": "test series", 
				"season": "test season", 
				"cat": ["IAB3"] 
			} 
		}, 
		"device": { 
			"ua": "Mozilla/5.0 (Linux; Android 4.4.4; Nexus 5 Build/KTU84P) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/33.0.0.0 Mobile Safari/537.36", 
			"os": "android", 
			"osv": "4.4.4", 
			"model": "SHV-E160K", 
			"ip": "123.145.167.189", 
			"ifa": "f5edbc38-2614-4470-927c-f182fc003411" 
		}, 
		"regs": { 
			"ext": { 
				"gdpr": 0 
			} 
		} 
	}
<br>

## Native
	{ 
		"id": "0m1hqt5x", 
		"imp": [{ 
			"id": "1001-2000-3000-4000", 
			"bidfloor": 0.03, 
			"native": { 
				"request": "{\"native\":{\"ver\":\"1.2\",\"assets\":[ ... ]}}", 
				"ver": "1.2", 
				"api": [3], 
				"battr": [13, 14] 
			} 
		}], 
		"app": { 
			"id": "78e87y2f284vry62", 
			"name": "test app", 
			"bundle": "com.app.test", 
			"storeurl": "http://test.test", 
			"cat": ["IAB3"] 
		}, 
		"device": { 
			"ua": "Mozilla/5.0 (Linux; Android 4.4.4; Nexus 5 Build/KTU84P) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/33.0.0.0 Mobile Safari/537.36", 
			"os": "android", 
			"osv": "4.4.4", 
			"model": "SHV-E160K", 
			"ip": "123.145.167.189", 
			"ifa": "f5edbc38-2614-4470-927c-f182fc003411" 
		}, 
		"regs": { 
			"ext": { 
				"gdpr": 0 
			} 
		} 
	} 
<br>

# 2. Bid Response Specification
## Object model

Object | Support | OpenRTB 2.3 Section for Reference | Extension
:--- | :---: | :---: | :---
BidResponse | O | 4.2.1 | X
SeatBid | O | 4.2.2 | X
Bid | O | 4.2.3 | X
<br>

## Object Specifications

- Object : BidResponse

Field name | Support
:--- | :---
id | O (Mandatory)
seatbid | O
bidid | O
cur | O (USD only)
customdata | X
nbr | X
ext | X
<br>

- Object : SeatBid

Field name | Support
:--- | :---
bid | O (Mandatory)
seat | O
group | X
ext | X
<br>

- Object : Bid

Field name | Support
:--- | :---
id | O (Mandatory)
impid | O (Mandatory)
price | O (Mandatory)
adid | X
nurl | X
adm | O (Mandatory), Format: HTML
adomain | O
bundle | X
iurl | O
cid | O
crid | O
cat | O
attr | X
dealid | X
h | O
w | O
ext | X
<br>

## Response sample

## Banner
	{ 
		"id": "0m1hqt5x", 
		"bidid": "abc1123", 
		"cur": "USD", 
		"seatbid": [{ 
			"seat": "512", 
			"bid": [{ 
				"id": "adxb_20151203171854390422024850", 
				"impid": "1", 
				"price": 1.2, 
				"adomain": ["aaa.com"], 
				"iurl": "http://test.com/image/aaa.jpg", 
				"crid": "1234", 
				"adm": "<a href=\"http://www.nasmedia.co.kr\" onclick=\"new Image().src='http://test.admixer.co.kr/click';new Image().src='${CLICK_TRACK_URL}';return true;\" target=\"_top\" style=\"text-decoration:none;\"><img id=\"ad\" src=\"http://test.admixer.co.kr/image.jpg\" style=\"width:320px;height:50px;border:0px;\"/></a><img src=\"http://test.admixer.co.kr/beacon?price=${AUCTION_PRICE}\" style=\"width:1px;height:1px;display:none;\" />" 
			}] 
		}] 
	} 
<br>

## Video
	{ 
		"id": "0m1hqt5x", 
		"bidid": "abc1123", 
		"cur": "USD", 
		"seatbid": [{ 
			"seat": "512", 
			"bid": [{ 
				"id": "adxb_20151203171854390422024850", 
				"impid": "1", 
				"price": 1.2, 
				"adomain": ["aaa.com"], 
				"crid": "1234", 
				"adm": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><VAST version=\"2.0\"></VAST>" 
			}] 
		}] 
	} 
<br>

## Native
	{ 
		"id": "0m1hqt5x", 
		"bidid": "abc1123", 
		"cur": "USD", 
		"seatbid": [{ 
			"seat": "512", 
			"bid": [{ 
				"id": "adxb_20151203171854390422024850", 
				"impid": "1", 
				"price": 1.2, 
				"adomain": ["aaa.com"], 
				"iurl": "http://test.com/image/aaa.jpg", 
				"crid": "1234", 
				"adm": "{\"native\":{\"ver\":\"1.0\",\"link\":{ ... }, \"imptrackers\":[ ... ],\"assets\":[ ... ]}}" 
			}] 
		}] 
	} 
<br>

## Substitution Macros

Macro | Explanation | Support
:--- | :---: | :---
${AUCTION_ID} | BidRequest.id | O
${AUCTION_BID_ID} | BidResponse.id | O
${AUCTION_IMP_ID} | win Imp.id | O
${AUCTION_SEAT_ID} | win SeatBid.seat | O
${AUCTION_AD_ID} | Bid.adid | O
${AUCTION_PRICE} | win Price | O
${AUCTION_PRICE:B64} | win Price (Base64 encoding) | O
${AUCTION_CURRENCY} | Currency of win price | O
${CLICK_TRACK_URL} | Click measurement URL | O
<br>

## Win notice

Method | Explanation
:--- | :---
Client-to-Server | Win notice URL must be included within Bid.adm.<br>SSP should replace macro of win-price Macro of win-price : ${AUCTION_PRICE}, ${AUCTION_PRICE:B64}
<br>

## Click measurement
If SSP wants click measurement, it is possible to follow below steps.
 1. When there is request, set 1 for value of **BidRequest.ext.clicktrack**
 2. Within responded **Bid.adm**, find macro of `${CLICK_TRACK_URL}`
 3. Replace this macro to click measurement URL of SSP. (No URL encoding)
 4. Replaced click measurement URL should respond with 1x1 pixel of image.

If SSP follows above steps, when click is made, replaced click measurement URL is called, and through this, SSP could know there was click.

