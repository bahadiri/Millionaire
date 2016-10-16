# Introduction
In order to develop effective crowdsourcing aggregation methods for multiple choice question answering(MCQA) and evaluate them empirically, we developed and deployed a crowdsourced system for playing the “Who wants to be a millionaire?” quiz show. This repository inludes our dataset in csv and sql formats.

# Data
Over the period of 9 months, we collected over 3 GB of data using our CrowdMillionaire app. In our dataset, there are 1908 questions and 214,658 unique answers to those
questions from CrowdMillionaire participants. In addition,
we have more than 5 million offline answers for archived live
questions.
Our dataset includes detailed information on the game
play. For example, our exhaustive timestamps show (1) how
much time it took for a question to arrive to a participant,
(2) when the question is actually presented to the participant
on her device, and (3) when exactly the participant answered
the question. We
shared this dataset in order
to advance the understanding of the MCQA dynamics, after we cleaned and anonymized the data.

# Citation
Please cite this publication http://research.microsoft.com/en-us/um/beijing/events/ms_ipsn13/papers/aydin.pdf 

Sample citation formats:
- Harvard
Aydin, B.I., Yilmaz, Y.S., Bulut, M.F. and Demirbas, M., Crowdreply: A crowdsourced multiple choice question answering system. In ACM/IEEE IPSN (Vol. 13).

- MLA
Aydin, Bahadir Ismail, et al. "Crowdreply: A crowdsourced multiple choice question answering system." ACM/IEEE IPSN. Vol. 13.

- BibTex entry
@inproceedings{aydin13crowdreply,
  title={Crowdreply: A crowdsourced multiple choice question answering system},
  author={Aydin, Bahadir Ismail and Yilmaz, Yavuz Selim and Bulut, Muhammed Fatih and Demirbas, Murat},
  booktitle={ACM/IEEE IPSN},
  volume={13}
}
