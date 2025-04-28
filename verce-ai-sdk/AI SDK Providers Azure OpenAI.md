[AI SDK Providers](https://sdk.vercel.ai/providers/ai-sdk-providers)Azure OpenAI

## [Azure OpenAI Provider](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#azure-openai-provider)

The [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai-service) provider contains language model support for the Azure OpenAI chat API.

## [Setup](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#setup)

The Azure OpenAI provider is available in the `@ai-sdk/azure` module. You can install it with

## [Provider Instance](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#provider-instance)

You can import the default provider instance `azure` from `@ai-sdk/azure`:

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> azure </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span></p></div>
```

If you need a customized setup, you can import `createAzure` from `@ai-sdk/azure` and create a provider instance with your settings:

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> createAzure </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> azure </span><span>=</span><span> </span><span>createAzure</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  resourceName</span><span>:</span><span> </span><span>'your-resource-name'</span><span>,</span><span> </span><span>// Azure resource name</span><span></span></p></div><div data-highlighted="false"><p><span>  apiKey</span><span>:</span><span> </span><span>'your-api-key'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

You can use the following optional settings to customize the OpenAI provider instance:

-   **resourceName** _string_
    
    Azure resource name. It defaults to the `AZURE_RESOURCE_NAME` environment variable.
    
    The resource name is used in the assembled URL: `https://{resourceName}.openai.azure.com/openai/deployments/{modelId}{path}`. You can use `baseURL` instead to specify the URL prefix.
    
-   **apiKey** _string_
    
    API key that is being sent using the `api-key` header. It defaults to the `AZURE_API_KEY` environment variable.
    
-   **apiVersion** _string_
    
    Sets a custom [api version](https://learn.microsoft.com/en-us/azure/ai-services/openai/api-version-deprecation). Defaults to `2024-10-01-preview`.
    
-   **baseURL** _string_
    
    Use a different URL prefix for API calls, e.g. to use proxy servers.
    
    Either this or `resourceName` can be used. When a baseURL is provided, the resourceName is ignored.
    
    With a baseURL, the resolved URL is `{baseURL}/{modelId}{path}`.
    
-   **headers** _Record<string,string>_
    
    Custom headers to include in the requests.
    
-   **fetch** _(input: RequestInfo, init?: RequestInit) => Promise<Response>_
    
    Custom [fetch](https://developer.mozilla.org/en-US/docs/Web/API/fetch) implementation. Defaults to the global `fetch` function. You can use it as a middleware to intercept requests, or to provide a custom fetch implementation for e.g. testing.
    

## [Language Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#language-models)

The Azure OpenAI provider instance is a function that you can invoke to create a language model:

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> </span><span>azure</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>;</span></p></div>
```

You need to pass your deployment name as the first argument.

### [Reasoning Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#reasoning-models)

Azure exposes the thinking of `DeepSeek-R1` in the generated text using the `<think>` tag. You can use the `extractReasoningMiddleware` to extract this reasoning and expose it as a `reasoning` property on the result:

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> azure </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>import</span><span> </span><span>{</span><span> wrapLanguageModel</span><span>,</span><span> extractReasoningMiddleware </span><span>}</span><span> </span><span>from</span><span> </span><span>'ai'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> enhancedModel </span><span>=</span><span> </span><span>wrapLanguageModel</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> </span><span>azure</span><span>(</span><span>'your-deepseek-r1-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  middleware</span><span>:</span><span> </span><span>extractReasoningMiddleware</span><span>(</span><span>{</span><span> tagName</span><span>:</span><span> </span><span>'think'</span><span> </span><span>}</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

You can then use that enhanced model in functions like `generateText` and `streamText`.

### [Example](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#example)

You can use OpenAI language models to generate text with the `generateText` function:

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> azure </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>import</span><span> </span><span>{</span><span> generateText </span><span>}</span><span> </span><span>from</span><span> </span><span>'ai'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> </span><span>{</span><span> text </span><span>}</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>generateText</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> </span><span>azure</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  prompt</span><span>:</span><span> </span><span>'Write a vegetarian lasagna recipe for 4 people.'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

OpenAI language models can also be used in the `streamText`, `generateObject`, and `streamObject` functions (see [AI SDK Core](https://sdk.vercel.ai/docs/ai-sdk-core)).

### [Provider Options](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#provider-options)

When using OpenAI language models on Azure, you can configure provider-specific options using `providerOptions.openai`. More information on available configuration options are on [the OpenAI provider page](https://sdk.vercel.ai/providers/ai-sdk-providers/openai#language-models).

```
<div data-highlighted="false"><p><span>const</span><span> messages </span><span>=</span><span> </span><span>[</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>    role</span><span>:</span><span> </span><span>'user'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>    content</span><span>:</span><span> </span><span>[</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>type</span><span>:</span><span> </span><span>'text'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>        text</span><span>:</span><span> </span><span>'What is the capital of the moon?'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>type</span><span>:</span><span> </span><span>'image'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>        image</span><span>:</span><span> </span><span>'https://example.com/image.png'</span><span>,</span><span></span></p></div><div data-highlighted="true"><p><span>        providerOptions</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="true"><p><span>          openai</span><span>:</span><span> </span><span>{</span><span> imageDetail</span><span>:</span><span> </span><span>'low'</span><span> </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="true"><p><span>        </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>]</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>]</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> </span><span>{</span><span> text </span><span>}</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>generateText</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> </span><span>azure</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="true"><p><span>  providerOptions</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="true"><p><span>    openai</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="true"><p><span>      reasoningEffort</span><span>:</span><span> </span><span>'low'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

### [Chat Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#chat-models)

The URL for calling Azure chat models will be constructed as follows: `https://RESOURCE_NAME.openai.azure.com/openai/deployments/DEPLOYMENT_NAME/chat/completions?api-version=API_VERSION`

Azure OpenAI chat models support also some model specific settings that are not part of the [standard call settings](https://sdk.vercel.ai/docs/ai-sdk-core/settings). You can pass them as an options argument:

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> </span><span>azure</span><span>(</span><span>'your-deployment-name'</span><span>,</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  logitBias</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>// optional likelihood for specific tokens</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>'50256'</span><span>:</span><span> </span><span>-</span><span>100</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  user</span><span>:</span><span> </span><span>'test-user'</span><span>,</span><span> </span><span>// optional unique user identifier</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

The following optional settings are available for OpenAI chat models:

-   **logitBias** _Record<number, number>_
    
    Modifies the likelihood of specified tokens appearing in the completion.
    
    Accepts a JSON object that maps tokens (specified by their token ID in the GPT tokenizer) to an associated bias value from -100 to 100. You can use this tokenizer tool to convert text to token IDs. Mathematically, the bias is added to the logits generated by the model prior to sampling. The exact effect will vary per model, but values between -1 and 1 should decrease or increase likelihood of selection; values like -100 or 100 should result in a ban or exclusive selection of the relevant token.
    
    As an example, you can pass `{"50256": -100}` to prevent the token from being generated.
    
-   **logprobs** _boolean | number_
    
    Return the log probabilities of the tokens. Including logprobs will increase the response size and can slow down response times. However, it can be useful to better understand how the model is behaving.
    
    Setting to true will return the log probabilities of the tokens that were generated.
    
    Setting to a number will return the log probabilities of the top n tokens that were generated.
    
-   **parallelToolCalls** _boolean_
    
    Whether to enable parallel function calling during tool use. Default to true.
    
-   **user** _string_
    
    A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. Learn more.
    

### [Responses Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#responses-models)

You can use the Azure OpenAI responses API with the `azure.responses(deploymentName)` factory method.

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>responses</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>;</span></p></div>
```

Further configuration can be done using OpenAI provider options. You can validate the provider options using the `OpenAIResponsesProviderOptions` type.

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> azure</span><span>,</span><span> </span><span>OpenAIResponsesProviderOptions</span><span> </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>import</span><span> </span><span>{</span><span> generateText </span><span>}</span><span> </span><span>from</span><span> </span><span>'ai'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> result </span><span>=</span><span> </span><span>await</span><span> </span><span>generateText</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> azure</span><span>.</span><span>responses</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  providerOptions</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>    openai</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>      parallelToolCalls</span><span>:</span><span> </span><span>false</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      store</span><span>:</span><span> </span><span>false</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      user</span><span>:</span><span> </span><span>'user_123'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>// ...</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>}</span><span> satisfies </span><span>OpenAIResponsesProviderOptions</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>// ...</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

The following provider options are available:

-   **parallelToolCalls** _boolean_ Whether to use parallel tool calls. Defaults to `true`.
    
-   **store** _boolean_ Whether to store the generation. Defaults to `true`.
    
-   **metadata** _Record<string, string>_ Additional metadata to store with the generation.
    
-   **previousResponseId** _string_ The ID of the previous response. You can use it to continue a conversation. Defaults to `undefined`.
    
-   **instructions** _string_ Instructions for the model. They can be used to change the system or developer message when continuing a conversation using the `previousResponseId` option. Defaults to `undefined`.
    
-   **user** _string_ A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. Defaults to `undefined`.
    
-   **reasoningEffort** _'low' | 'medium' | 'high'_ Reasoning effort for reasoning models. Defaults to `medium`. If you use `providerOptions` to set the `reasoningEffort` option, this model setting will be ignored.
    
-   **strictSchemas** _boolean_ Whether to use strict JSON schemas in tools and when generating JSON outputs. Defaults to `true`.
    

The Azure OpenAI responses provider also returns provider-specific metadata:

```
<div data-highlighted="false"><p><span>const</span><span> </span><span>{</span><span> providerMetadata </span><span>}</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>generateText</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> azure</span><span>.</span><span>responses</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> openaiMetadata </span><span>=</span><span> providerMetadata</span><span>?.</span><span>openai</span><span>;</span></p></div>
```

The following OpenAI-specific metadata is returned:

-   **responseId** _string_ The ID of the response. Can be used to continue a conversation.
    
-   **cachedPromptTokens** _number_ The number of prompt tokens that were a cache hit.
    
-   **reasoningTokens** _number_ The number of reasoning tokens that the model generated.
    

#### [Web Search](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#web-search)

The Azure OpenAI responses provider supports web search through the `azure.tools.webSearchPreview` tool.

You can force the use of the web search tool by setting the `toolChoice` parameter to `{ type: 'tool', toolName: 'web_search_preview' }`.

```
<div data-highlighted="false"><p><span>const</span><span> result </span><span>=</span><span> </span><span>await</span><span> </span><span>generateText</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> azure</span><span>.</span><span>responses</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  prompt</span><span>:</span><span> </span><span>'What happened in San Francisco last week?'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  tools</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>    web_search_preview</span><span>:</span><span> azure</span><span>.</span><span>tools</span><span>.</span><span>webSearchPreview</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>// optional configuration:</span><span></span></p></div><div data-highlighted="false"><p><span>      searchContextSize</span><span>:</span><span> </span><span>'high'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      userLocation</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>type</span><span>:</span><span> </span><span>'approximate'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>        city</span><span>:</span><span> </span><span>'San Francisco'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>        region</span><span>:</span><span> </span><span>'California'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>}</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>// Force web search tool:</span><span></span></p></div><div data-highlighted="false"><p><span>  toolChoice</span><span>:</span><span> </span><span>{</span><span> </span><span>type</span><span>:</span><span> </span><span>'tool'</span><span>,</span><span> toolName</span><span>:</span><span> </span><span>'web_search_preview'</span><span> </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>// URL sources</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> sources </span><span>=</span><span> result</span><span>.</span><span>sources</span><span>;</span></p></div>
```

#### [PDF support](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#pdf-support)

The Azure OpenAI Responses API supports reading PDF files. You can pass PDF files as part of the message content using the `file` type:

```
<div data-highlighted="false"><p><span>const</span><span> result </span><span>=</span><span> </span><span>await</span><span> </span><span>generateText</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> azure</span><span>.</span><span>responses</span><span>(</span><span>'your-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  messages</span><span>:</span><span> </span><span>[</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>      role</span><span>:</span><span> </span><span>'user'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      content</span><span>:</span><span> </span><span>[</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>          </span><span>type</span><span>:</span><span> </span><span>'text'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>          text</span><span>:</span><span> </span><span>'What is an embedding model?'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>          </span><span>type</span><span>:</span><span> </span><span>'file'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>          data</span><span>:</span><span> fs</span><span>.</span><span>readFileSync</span><span>(</span><span>'./data/ai.pdf'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>          mimeType</span><span>:</span><span> </span><span>'application/pdf'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>          filename</span><span>:</span><span> </span><span>'ai.pdf'</span><span>,</span><span> </span><span>// optional</span><span></span></p></div><div data-highlighted="false"><p><span>        </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>      </span><span>]</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>]</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

The model will have access to the contents of the PDF file and respond to questions about it. The PDF file should be passed using the `data` field, and the `mimeType` should be set to `'application/pdf'`.

### [Completion Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#completion-models)

You can create models that call the completions API using the `.completion()` factory method. The first argument is the model id. Currently only `gpt-35-turbo-instruct` is supported.

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>completion</span><span>(</span><span>'your-gpt-35-turbo-instruct-deployment'</span><span>)</span><span>;</span></p></div>
```

OpenAI completion models support also some model specific settings that are not part of the [standard call settings](https://sdk.vercel.ai/docs/ai-sdk-core/settings). You can pass them as an options argument:

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>completion</span><span>(</span><span>'your-gpt-35-turbo-instruct-deployment'</span><span>,</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  echo</span><span>:</span><span> </span><span>true</span><span>,</span><span> </span><span>// optional, echo the prompt in addition to the completion</span><span></span></p></div><div data-highlighted="false"><p><span>  logitBias</span><span>:</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>// optional likelihood for specific tokens</span><span></span></p></div><div data-highlighted="false"><p><span>    </span><span>'50256'</span><span>:</span><span> </span><span>-</span><span>100</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  suffix</span><span>:</span><span> </span><span>'some text'</span><span>,</span><span> </span><span>// optional suffix that comes after a completion of inserted text</span><span></span></p></div><div data-highlighted="false"><p><span>  user</span><span>:</span><span> </span><span>'test-user'</span><span>,</span><span> </span><span>// optional unique user identifier</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

The following optional settings are available for Azure OpenAI completion models:

-   **echo**: _boolean_
    
    Echo back the prompt in addition to the completion.
    
-   **logitBias** _Record<number, number>_
    
    Modifies the likelihood of specified tokens appearing in the completion.
    
    Accepts a JSON object that maps tokens (specified by their token ID in the GPT tokenizer) to an associated bias value from -100 to 100. You can use this tokenizer tool to convert text to token IDs. Mathematically, the bias is added to the logits generated by the model prior to sampling. The exact effect will vary per model, but values between -1 and 1 should decrease or increase likelihood of selection; values like -100 or 100 should result in a ban or exclusive selection of the relevant token.
    
    As an example, you can pass `{"50256": -100}` to prevent the <|endoftext|> token from being generated.
    
-   **logprobs** _boolean | number_
    
    Return the log probabilities of the tokens. Including logprobs will increase the response size and can slow down response times. However, it can be useful to better understand how the model is behaving.
    
    Setting to true will return the log probabilities of the tokens that were generated.
    
    Setting to a number will return the log probabilities of the top n tokens that were generated.
    
-   **suffix** _string_
    
    The suffix that comes after a completion of inserted text.
    
-   **user** _string_
    
    A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. Learn more.
    

## [Embedding Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#embedding-models)

You can create models that call the Azure OpenAI embeddings API using the `.embedding()` factory method.

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>embedding</span><span>(</span><span>'your-embedding-deployment'</span><span>)</span><span>;</span></p></div>
```

Azure OpenAI embedding models support several additional settings. You can pass them as an options argument:

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>embedding</span><span>(</span><span>'your-embedding-deployment'</span><span>,</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  dimensions</span><span>:</span><span> </span><span>512</span><span> </span><span>// optional, number of dimensions for the embedding</span><span></span></p></div><div data-highlighted="false"><p><span>  user</span><span>:</span><span> </span><span>'test-user'</span><span> </span><span>// optional unique user identifier</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span></p></div>
```

The following optional settings are available for Azure OpenAI embedding models:

-   **dimensions**: _number_
    
    The number of dimensions the resulting output embeddings should have. Only supported in text-embedding-3 and later models.
    
-   **user** _string_
    
    A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. Learn more.
    

## [Image Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#image-models)

You can create models that call the Azure OpenAI image generation API (DALL-E) using the `.imageModel()` factory method. The first argument is your deployment name for the DALL-E model.

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>imageModel</span><span>(</span><span>'your-dalle-deployment-name'</span><span>)</span><span>;</span></p></div>
```

Azure OpenAI image models support several additional settings. You can pass them as an options argument:

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>imageModel</span><span>(</span><span>'your-dalle-deployment-name'</span><span>,</span><span> </span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  user</span><span>:</span><span> </span><span>'test-user'</span><span>,</span><span> </span><span>// optional unique user identifier</span><span></span></p></div><div data-highlighted="false"><p><span>  responseFormat</span><span>:</span><span> </span><span>'url'</span><span>,</span><span> </span><span>// 'url' or 'b64_json', defaults to 'url'</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

### [Example](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#example-1)

You can use Azure OpenAI image models to generate images with the `generateImage` function:

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> azure </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>import</span><span> </span><span>{</span><span> experimental_generateImage </span><span>as</span><span> generateImage </span><span>}</span><span> </span><span>from</span><span> </span><span>'ai'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> </span><span>{</span><span> image </span><span>}</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>generateImage</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="false"><p><span>  model</span><span>:</span><span> azure</span><span>.</span><span>imageModel</span><span>(</span><span>'your-dalle-deployment-name'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  prompt</span><span>:</span><span> </span><span>'A photorealistic image of a cat astronaut floating in space'</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  size</span><span>:</span><span> </span><span>'1024x1024'</span><span>,</span><span> </span><span>// '1024x1024', '1792x1024', or '1024x1792' for DALL-E 3</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>// image contains the URL or base64 data of the generated image</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>console</span><span>.</span><span>log</span><span>(</span><span>image</span><span>)</span><span>;</span></p></div>
```

### [Model Capabilities](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#model-capabilities)

Azure OpenAI supports DALL-E 2 and DALL-E 3 models through deployments. The capabilities depend on which model version your deployment is using:

| Model Version | Sizes |
| --- | --- |
| DALL-E 3 | 1024x1024, 1792x1024, 1024x1792 |
| DALL-E 2 | 256x256, 512x512, 1024x1024 |

DALL-E models do not support the `aspectRatio` parameter. Use the `size` parameter instead.

When creating your Azure OpenAI deployment, make sure to set the DALL-E model version you want to use.

## [Transcription Models](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#transcription-models)

You can create models that call the Azure OpenAI transcription API using the `.transcription()` factory method.

The first argument is the model id e.g. `whisper-1`.

```
<div data-highlighted="false"><p><span>const</span><span> model </span><span>=</span><span> azure</span><span>.</span><span>transcription</span><span>(</span><span>'whisper-1'</span><span>)</span><span>;</span></p></div>
```

You can also pass additional provider-specific options using the `providerOptions` argument. For example, supplying the input language in ISO-639-1 (e.g. `en`) format will improve accuracy and latency.

```
<div data-highlighted="false"><p><span>import</span><span> </span><span>{</span><span> experimental_transcribe </span><span>as</span><span> transcribe </span><span>}</span><span> </span><span>from</span><span> </span><span>'ai'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>import</span><span> </span><span>{</span><span> azure </span><span>}</span><span> </span><span>from</span><span> </span><span>'@ai-sdk/azure'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>import</span><span> </span><span>{</span><span> readFile </span><span>}</span><span> </span><span>from</span><span> </span><span>'fs/promises'</span><span>;</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>const</span><span> result </span><span>=</span><span> </span><span>await</span><span> </span><span>transcribe</span><span>(</span><span>{</span><span></span></p></div><div data-highlighted="true"><p><span>  model</span><span>:</span><span> azure</span><span>.</span><span>transcription</span><span>(</span><span>'whisper-1'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  audio</span><span>:</span><span> </span><span>await</span><span> </span><span>readFile</span><span>(</span><span>'audio.mp3'</span><span>)</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span>  providerOptions</span><span>:</span><span> </span><span>{</span><span> azure</span><span>:</span><span> </span><span>{</span><span> language</span><span>:</span><span> </span><span>'en'</span><span> </span><span>}</span><span> </span><span>}</span><span>,</span><span></span></p></div><div data-highlighted="false"><p><span></span><span>}</span><span>)</span><span>;</span></p></div>
```

The following provider options are available:

-   **timestampGranularities** _string\[\]_ The granularity of the timestamps in the transcription. Defaults to `['segment']`. Possible values are `['word']`, `['segment']`, and `['word', 'segment']`. Note: There is no additional latency for segment timestamps, but generating word timestamps incurs additional latency.
    
-   **language** _string_ The language of the input audio. Supplying the input language in ISO-639-1 format (e.g. 'en') will improve accuracy and latency. Optional.
    
-   **prompt** _string_ An optional text to guide the model's style or continue a previous audio segment. The prompt should match the audio language. Optional.
    
-   **temperature** _number_ The sampling temperature, between 0 and 1. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. If set to 0, the model will use log probability to automatically increase the temperature until certain thresholds are hit. Defaults to 0. Optional.
    
-   **include** _string\[\]_ Additional information to include in the transcription response.
    

### [Model Capabilities](https://sdk.vercel.ai/providers/ai-sdk-providers/azure#model-capabilities-1)

| Model | Transcription | Duration | Segments | Language |
| --- | --- | --- | --- | --- |
| `whisper-1` |  |  |  |  |
| `gpt-4o-mini-transcribe` |  |  |  |  |
| `gpt-4o-transcribe` |  |  |  |  |