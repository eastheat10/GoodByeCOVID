# GoodBye Corona
* [GoodBye Corona API](https://api.corona-19.kr/)
* Alamofire
* Charts
를 이용한 국내 코로나 현황판

<img src="https://user-images.githubusercontent.com/38150034/147679338-7179c993-6428-487d-859c-2f2e729c2494.png" width="200px" />
<img src="https://user-images.githubusercontent.com/38150034/147679380-1e034682-975c-42c5-b673-ce6ecc2fe9ab.png" width="200px" />

* Alamofire
* Charts

```swift
func fetchCovidOverView(completionHandler: @escaping (Result<CityCovidOverview, Error>) -> Void) {
	let url = "https://api.corona-19.kr/korea/country/new/"
	let param = [
		"serviceKey": {API Key}
	]

	AF.request(url, method: .get, parameters: param)
		.responseData(completionHandler: { response in
		switch response.result {
		case let .success(data):
			do {
				let decoder = JSONDecoder()
				let result = try decoder.decode(CityCovidOverview.self, from: data)
			completionHandler(.success(result))
			} catch {
				completionHandler(.failure(error))
			}
			case let .failure(error):
				completionHandler(.failure(error))
		}
	})
}
```
