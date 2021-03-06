.. index:: pair: page; Introduction to Performance Optimization
.. _doxid-openvino_docs_optimization_guide_dldt_optimization_guide:


Introduction to Performance Optimization
========================================

:target:`doxid-openvino_docs_optimization_guide_dldt_optimization_guide_1md_openvino_docs_optimization_guide_dldt_optimization_guide` Even though inference performance should be defined as a combination of many factors, including accuracy and efficiency, it is most often described as the speed of execution. As the rate with which the model processes live data, it is based on two fundamentally interconnected metrics: latency and throughput.

.. image:: LATENCY_VS_THROUGHPUT.svg

**Latency** measures inference time (in ms) required to process a single input. When it comes to executing multiple inputs simultaneously (for example, via batching), the overall throughput (inferences per second, or frames per second, FPS, in the specific case of visual processing) is usually more of a concern. **Throughput** is calculated by dividing the number of inputs that were processed by the processing time.

End-to-End Application Performance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is important to separate the "pure" inference time of a neural network and the end-to-end application performance. For example, data transfers between the host and a device may unintentionally affect the performance when a host input tensor is processed on the accelerator such as dGPU.

Similarly, the input-preprocessing contributes significantly to the inference time. As described in the :ref:`getting performance numbers <doxid-openvino_docs__m_o__d_g__getting__performance__numbers>` section, when evaluating *inference* performance, one option is to measure all such items separately. For the **end-to-end scenario**, though, consider image pre-processing with OpenVINO and the asynchronous execution as a way to lessen the communication costs (like data transfers). For more details, see the :ref:`general optimizations guide <doxid-openvino_docs_deployment_optimization_guide_common>`.

Another specific case is **first-inference latency** (for example, when a fast application start-up is required), where the resulting performance may be well dominated by the model loading time. :ref:`Model caching <doxid-openvino_docs__o_v__u_g__model_caching_overview>` may be considered as a way to improve model loading/compilation time.

Finally, **memory footprint** restriction is another possible concern when designing an application. While this is a motivation for the use of the *model* optimization techniques, keep in mind that the throughput-oriented execution is usually much more memory consuming. For more details, see the :ref:`Runtime Inference Optimizations guide <doxid-openvino_docs_deployment_optimization_guide_dldt_optimization_guide>`.

.. note:: To get performance numbers for OpenVINO, along with the tips on how to measure and compare it with a native framework, see the :ref:`Getting performance numbers article <doxid-openvino_docs__m_o__d_g__getting__performance__numbers>`.





Improving Performance: Model vs Runtime Optimizations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: First, make sure that your model can be successfully inferred with OpenVINO Runtime.



There are two primary optimization approaches to improving inference performance with OpenVINO: model- and runtime-level optimizations. They are **fully compatible** and can be done independently.

* **Model optimizations** include model modifications, such as quantization, pruning, optimization of preprocessing, etc. For more details, refer to this :ref:`document <doxid-openvino_docs_model_optimization_guide>`.
  
  * The model optimizations directly improve the inference time, even without runtime parameters tuning (described below).

* **Runtime (Deployment) optimizations** includes tuning of model *execution* parameters. Fore more details, see the :ref:`Runtime Inference Optimizations guide <doxid-openvino_docs_deployment_optimization_guide_dldt_optimization_guide>`.

Performance benchmarks
~~~~~~~~~~~~~~~~~~~~~~

A wide range of public models for estimating performance and comparing the numbers (measured on various supported devices) are available in the :ref:`Performance benchmarks section <doxid-openvino_docs_performance_benchmarks>`.

