# Amazon SageMaker Debugger Exceptions<a name="debugger-exceptions"></a>

Amazon SageMaker Debugger is designed to be aware that tensors required to execute a rule may not be available at every step\. Hence it raises a few exceptions which allow us to control what happens when a tensor is missing\. There are These are available in the [smdebug\.exceptions module](https://github.com/awslabs/sagemaker-debugger/blob/master/smdebug/exceptions.py)\. You can import them as follows:

```
from smdebug.exceptions import *
```

Here are the exceptions and their meanings:
+ `TensorUnavailableForStep`: The tensor requested is not available for the step\. This might mean that this step might not be saved at all by the hook, or that this step might have saved some tensors but the requested tensor is not part of them\. Note that when you see this exception, it means that this tensor can never become available for this step in the future\. If the tensor has reductions saved for the step, it notifies you they can be queried\.
+ `TensorUnavailable`: This tensor is not being saved or has not been saved by the smdebug API\. This means that this tensor will never be seen for any step in smdebug\.
+ `StepUnavailable`: The step was not saved and Debugger has no data from the step\.
+ `StepNotYetAvailable`: The step has not yet been seen by smdebug\. It may be available in the future if the training is still going on\. Debugger automatically loads new data as and when it becomes available\.
+ `NoMoreData`: Raised when the training ends\. Once you see this, you know that there are no more steps and no more tensors to be saved\.
+ `IndexReaderException`: The index reader is not valid\.
+ `InvalidWorker`: A worker was invoked that was not valid\.
+ `RuleEvaluationConditionMet`: Evaluation of the rule at the step resulted in the condition being met"
+ `InsufficientInformationForRuleInvocation`: Insufficient information was provided to invoke the rule\.