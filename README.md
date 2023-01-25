# Jointly-Learnt Networks for Future Action Anticipation via Self-Knowledge Distillation and Cycle Consistency

# Abstract
<p align="justify">Future action anticipation aims to infer future actions from the observation of a small set of past video frames. In this paper, we propose a novel Jointly-learnt Action Anticipation Network (J-AAN) via Self-Knowledge Distillation (Self-KD) and cycle consistency for future action anticipation. In contrast to the current state-of-the-art methods which anticipate the future actions either directly or recursively, our proposed J-AAN anticipates the future actions jointly in both direct and recursive ways. However, when dealing with future action anticipation, one important challenge to address is the future’s uncertainty since multiple action sequences may come from or be followed by the same action. Training an action anticipation model with one-hot-encoded hard labels that assign zero probabilities to incorrect yet semantically similar actions may not handle the uncertain future. To address this challenge, we design a Self-KD mechanism to train our J-AAN, where the J-AAN gradually distills its own knowledge during the training to soften the hard labels to model the uncertainty on future action anticipation. Furthermore, we design a forward and backward action anticipation framework with our proposed J-AAN based on a cyclic consistency constraint. The forward J-AAN anticipates the future actions from the observed past actions, and the backward J-AAN verifies the anticipation of the forward JAAN by anticipating the past actions from the anticipated future actions. The proposed method outperforms all the latest state-ofthe-art action anticipation methods on the Breakfast, 50Salads, and EPIC-Kitchens-55 datasets.</p>

# Main ideas
![idea_1](https://user-images.githubusercontent.com/59179258/214524973-cfd4dd62-7a81-4965-bba1-dc28eba63b1a.svg)
![idea_23](https://user-images.githubusercontent.com/59179258/214524985-41815232-0615-4aa0-8987-1b3a58cbc516.svg)
<p align="justify">Illustration of our three main ideas: (a) Jointly-learnt Action Anticipation Network (J-AAN) that anticipates the future actions from the observed past actions in both direct and recursive ways; (b) Self-knowledge distillation mechanism to train the J-AAN, where the J-AAN gradually distills its own knowledge during training; and (c) Forward and backward J-AANs with cycle consistency, where the backward J-AAN evaluates how well the forward JAAN anticipates the future actions by anticipating the past actions from the anticipated future actions.</p>

# Overview
![overview](https://user-images.githubusercontent.com/59179258/214522222-18c03ee3-696e-4d3c-bee4-8604fb7e961a.svg)
<p align="justify">Overview of our proposed Jointly-learnt Action Anticipation Network (J-AAN) for future action anticipation via Self-Knowledge Distillation (Self-KD) and cycle consistency. During the training, it consists of two networks, a forward network, and a backward network. Both the forward and backward networks are constructed with our proposed J-AAN. The forward J-AAN anticipates the future actions from the observed frame-wise past actions, and gradually distills its own knowledge to soften the hard labels during the training to handle the uncertainty of future actions. The backward J-AAN takes the anticipated future actions from the forward J-AAN as an input to anticipate the past actions, satisfying a cyclic consistency constraint, in the sense that if the forward J-AAN can accurately anticipate the future actions from the past actions, then the backward J-AAN is expected to translate it back from the future actions to the past actions. During the testing, we only use the forward J-AAN to anticipate future actions.</p>

# The action representation generation for the forward J-AAN and the backward J-AAN
![action_representation](https://user-images.githubusercontent.com/59179258/214522785-3364a907-2b58-4d0a-93a2-17b7b7bd0f71.svg)

# Jointly-learnt Action Anticipation Network (J-AAN)
![encoder_decoder](https://user-images.githubusercontent.com/59179258/214523130-aa243961-d93a-4672-af06-2f0c594ca2a4.svg)
<p align="justify">Illustration of our proposed Jointly-learnt Action Anticipation Network (J-AAN). The J-AAN contains a recurrent encoder, a direct anticipation module, and a recursive anticipation module. The recurrent encoder encodes the frame-wise actions over different time steps of the observed frames. The direct anticipation module takes the encoded features and directly anticipates all the actions and their corresponding duration, while the recursive anticipation contains a recursive initialization and a recurrent decoder to recursively anticipate the future actions and their duration. During the recursive anticipation, the recurrent decoder takes the anticipated actions from the direct anticipation as one of the inputs for better future action anticipation.</p>

# Cycle consistency
![cycle](https://user-images.githubusercontent.com/59179258/214523593-44dde127-f445-4558-a8f7-1cb410ba09fc.svg)
<p align="justify">Illustration of our proposed forward and backward J-AANs. The forward J-AAN anticipates the forward future actions and their duration from the forward frame-wise past actions. The anticipated future actions are stacked in a matrix according to their duration to get the forward frame-wise future actions, which is then reversed in temporal domain to get the backward frame-wise future actions. The backward J-AAN loads the backward frame-wise future actions and anticipates the backward past actions and their corresponding duration, which satisfies a cycle consistency. Note that, both the forward J-AAN and the backward J-AAN perform their corresponding anticipation jointly in both direct and recursive ways. For the simplicity, we show the output of the recursive anticipation for each J-AAN.</p>

# Qualitative analysis

## Importance of Jointly-learnt Action Anticipation Network (J-AAN)
![qual_jaan](https://user-images.githubusercontent.com/59179258/214523949-bc8086ab-367b-4701-b0c8-d3289ce0be16.svg)
<p align="justify">Importance of Jointly-learnt Action Anticipation Network (J-AAN). The J-AAN anticipates the future action jointly in both direct and recursive ways. The joint learning of these two anticipation approaches performs better action anticipation compared to the individual ones. The model observes the first 30% of the video and anticipates the frame-wise actions of following 50% of that video. (GT: ground truth).</p>

## Impact of the Self-Knowledge Distillation (Self-KD) mechanism
![qual_skd](https://user-images.githubusercontent.com/59179258/214524044-31b06407-577b-4367-8bd6-079dba0b7049.svg)
<p align="justify">Impact of the Self-Knowledge Distillation (Self-KD) mechanism. Both actions “pour coffee” and “spoon powder” follow the same observed actions. The J-AAN trained without Self-KD mechanism anticipates the same action for both cases. The Self-KD mechanism can handle this uncertainty on the future action anticipation. The model observes the first 30% of the video and anticipates the frame-wise actions of following 50% of that video. (GT: ground truth).</p>

## Impact of the cycle consistency loss
![qual_cyc](https://user-images.githubusercontent.com/59179258/214523982-dfb7b807-64bf-43b0-b4f8-0162b8cecca6.svg)
<p align="justify">Impact of the cycle consistency loss. By anticipating the past actions from the anticipated future actions, the cycle consistency verifies whether the complete set of the future actions are anticipated or not. Without the cycle consistency loss, the J-AAN missed to anticipate the “add oil” action. The cycle consistency resolves this issue. The model observes the first 30% of the video and anticipates the frame-wise actions of following 50% of that video.</p>

# Citation:
If you find our work useful for your research, please cite our work:

```latex
@article{moniruzzaman2022jointly,
  title={Jointly-Learnt Networks for Future Action Anticipation via Self-Knowledge Distillation and Cycle Consistency},
  author={Moniruzzaman, Md and Yin, Zhaozheng and He, Zhihai and Leu, Ming C and Qin, Ruwen},
  journal={IEEE Transactions on Circuits and Systems for Video Technology},
  year={2022},
  publisher={IEEE}
}
```

# Contact 
If you have any question or comment, please contact the first author of this paper -- Md Moniruzzaman 
