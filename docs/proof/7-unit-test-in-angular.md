# Unit Testing in a frontend Angular web app

- [Unit Testing in a frontend Angular web app](#unit-testing-in-a-frontend-angular-web-app)
- [Intro](#intro)
  - [Karma and Jasmine](#karma-and-jasmine)
  - [Unit Testing a Service](#unit-testing-a-service)

# Intro

Unit testing is an important part of backend development, but many people forget it is also important in frontend development. Every Javascript-based frontend has some kind of conditional logic applied to it, which can go wrong. You can write tests to safeguard your application, the same way you would do with your backend logic.

## Karma and Jasmine

Angular primarily uses the Karma framework with Jasmine to provide a testing framework. You can learn more about them here:

- [Karma](https://karma-runner.github.io/6.4/index.html)
- [Jasmine](https://jasmine.github.io/)

## Unit Testing a Service

Imagine you have defined an Angular service like this:

```ts
export class GoogleApiService {
  constructor(
    private readonly oAuthService: OAuthService,
    private readonly httpClient: HttpClient
  ) {  }

async getEmailIds(userId: string, queryParams: HttpParams): Promise<string[]> {
  const messageIdResponse = await lastValueFrom(this.httpClient.get(
      `${this.gmailBaseUrl}${userId}/messages`,
      {params: queryParams}
  ) as Observable<GmailMessageIdResponse>)

  if (!messageIdResponse || !messageIdResponse.messages || messageIdResponse?.messages?.length <= 0) {
      return []
  }

  return messageIdResponse.messages.map(function (mip) {
      return mip.id
  })
}
```

This service has the dependencies (uh oh) of `OAuthService` and `HttpClient`, and currently only has a function to get a list of ids from a foreign endpoint.

Angular uses `TestBed` to inject dependencies into the tests, and has a handy `HttpClientTestingModule` for mocking the `HttpClient`. To mock the OAuthService, we have to provide our own mocking class:

```ts
class MockAuthService {
  hasValidAccessToken() { return true }

  revokeTokenAndLogout(): Promise<any> { return Promise.all([]) }

  configure(): void { }

  loadDiscoveryDocument(): Promise<any> { return Promise.resolve() }

  tryLoginImplicitFlow(): Promise<boolean> { return Promise.resolve(true) }

  loadUserProfile(): Promise<UserInformation> {
    return Promise.resolve({
      info: {
        sub: 'hello',
        email: 'hello@world.com',
        given_name: 'Test',
        family_name: 'Guy',
        picture: 'https://www.example.com'
      }
    } as UserInformation)
  }

  initLoginFlow(): void { }
}
```

`Jasmine` uses the `describe` and `it` functions to make the tests more readable. 

```ts
function resultAsserts(
      expectedLength: number,
      expectedResult: string[],
      actualResult: string[]
    ): void {
  // Assert
  expect(actualResult).toBeTruthy()
  expect(actualResult.length).toEqual(expectedLength)
  expect(actualResult).toEqual(expectedResult)
}

it('should return the ids when Google responds with a valid response',
  inject([HttpClient], async (http: HttpClient) => {

    // Arrange
    const expectedResponseBody = {
      messages: [
        {id: 'test1', threadId: 'testThread1'} as GmailMessageIdPair,
        {id: 'test2', threadId: 'testThread2'} as GmailMessageIdPair
      ] as GmailMessageIdPair[],
      nextPageToken: 'testToken',
      resulSizeEstimate: 0
    } as GmailMessageIdResponse
    spyOn(http, 'get').and.returnValue(of(expectedResponseBody))

    // Act
    const result = await googleApiService.getEmailIds('test', new HttpParams())

    // Assert
    resultAsserts(
      expectedResponseBody.messages.length,
      expectedResponseBody.messages.map(function (mip) {
        return mip.id
      }),
      result
    )
  }))
```

With `spyOn` you can mock a function being called, and provide a return value the service can handle. This way, we can isolate the service enough, and have no dependencies to rely on.

The act and assert actions are as you would expect from any other testing framework. It `expect`s `x` to be `y`.