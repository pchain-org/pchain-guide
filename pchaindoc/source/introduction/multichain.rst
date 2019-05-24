===========
Multi Chain
===========

Multi-chain is the organization structure of co-existing chains in pchain, it contains one main chain and necessary number of parallel child chains.

--------------------------------------------
responsibilities of different types of chain
--------------------------------------------
| Pchain has two types of chains, one is main chain, there is only one main chain in pchain; another is child-chain, there could be many, and they are identical and independent.

| Main chain is responsible for balance record/transfer, and storage of child-chains’ data. Child is responsible for running smart contract. For both main chain and child chains, PAI(pchain’s token) is paid for their transaction execution. PAI in mains and child chains have the same value, and can be transferred between main chain and child chains.

----------------------
design of multi-chain
----------------------
- every chain has its own stack(consensus, transaction, block, EVM)

	In pchain, main chain and child chains run their stacks individually, these stacks share same logic for most modules, such as consensus algorithm(PDBFT), receive and process of transaction, storage of block, execution of EVM, etc.

	The difference between main chain’s stack and child chain’s stack is: the stack of main chain limits deployment of smart contract; the stack of child chains does not issue their own token, main chain and child chains share one PAI.

- rpc

    Pchain writes specific RPC logic for multi-chain, every child handles its own RPC requirements individually. When calling, it just needs adding chain id in url’s path to differentiate the chain. For example, when access child chain ‘childchain-0’, the url to POST is http://pchain-node/childchain-0.

- p2p

    By taking advantage of design of ethereum’s P2P module, when initials and starts one chain, simply adding the mapping of chain and one sub protocol(just supplies a name) into ProtocolManager will make p2p messages are correctly routed within related chains.

- chain manager and cross-chain helper

    There are 2 entities outside the stacks coordinating the chains. One is ChainManager, which holds all chain’s information such as epochs and their validators, and also manages the initialing/start process of all chain.

    Another is CrossChainHelper, which is injected into every chain’s stack. When main/child chain needs to retrieve cross-chain information or call cross-chain functions, CrossChainHelper will come in handy.

----------------------------
what multi-chain can supply
----------------------------
- Easily create company’s own chain

    Any company has enough PAI and enough valitadors can create one child-chain in pchain. And this child chain would act as a normal public chain or consortium chain, the company will get all features blockchain technology supplies.

- multi-chain can co-operate together to achieve large scale business logic

    Because every single chain has its own process power, when business modules can be split apart and independent to each other, then every module can be deployed in one chain. By this way, even very large business can run on pchain with collaborating its modules on different chains.


