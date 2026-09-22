The Beautiful Game

Communications & Social Layer Appendix v0.1

An implementation appendix to the Information, Media & Communication Constitution v1.3.

Status — groundwork / implementation baseline. This appendix defines the domain boundary for in-world social communication before implementation. It is subordinate to the Constitution and may not override the privacy, participation, determinism or information-leakage rules defined there.

---

Design Principle

Conversation describes, accompanies and connects the football world. Structured actions change it.

The communication layer may make the world feel alive, social and inhabited. It may never become a second game engine, a shadow transfer system, a hidden source of player knowledge or a mechanism that rewards being constantly online.

---

1. Scope

The communications layer covers:

- public and scoped discussion between managers;
- private manager-to-manager conversations;
- discussion attached to canonical game objects;
- manager-visible system and game-actor messages;
- transfer and recruitment listings;
- unread/read state and notification routing;
- moderation, blocking and reporting;
- optional feed publication of information already public by constitutional rule.

It does not own match resolution, transfers, contracts, appointments, scouting, player decisions, board decisions, press effects, professionalism, sanctions or any other authoritative game state.

---

2. Identity

Every human participant uses the authoritative TBG manager identity.

No separate chat identity is created. Display names, club appointments and eligibility derive from TBG canonical state.

System actors — including agents, boards, journalists, clubs and competition authorities — must always be visibly distinguishable from human managers. The interface must never imply that generated or system-authored content was written by another human manager.

Identity survives club changes. A manager conversation belongs to the manager identities involved, not to the clubs they happened to control when it began, unless the conversation is explicitly club-scoped by design.

---

3. Conversation Scopes

The baseline scopes are:

Private — visible only to explicit participants and authorised system processes.

Club — visible to the current manager and any constitutionally authorised club actors or staff.

Competition — visible to managers eligible for that competition or division.

World — visible to all authenticated managers in the world.

Object Discussion — inherits an explicit visibility policy from the bound canonical object.

A later implementation may add additional scopes, but every scope must have a server-enforced visibility rule. Hidden navigation is never access control.

---

4. Canonical Objects

Conversation may attach to canonical TBG objects including:

- manager;
- club;
- player;
- fixture;
- competition;
- news item;
- transfer listing;
- recruitment listing;
- vacancy;
- manager approach;
- transfer enquiry or negotiation.

Object identity uses durable TBG type and identifier pairs, not display names or mutable page URLs.

Example:

object_type = "player"
object_id = "<canonical player id>"

A page URL may be stored as presentation metadata, but it is never the authoritative relationship.

---

5. Conversation Model

The minimum private-conversation model is:

conversations
- id
- world_id
- conversation_type
- object_type (optional)
- object_id (optional)
- created_at
- closed_at (optional)

conversation_members
- conversation_id
- manager_id
- joined_at
- last_read_at
- muted_at (optional)
- left_at (optional)

conversation_messages
- id
- conversation_id
- sender_manager_id (nullable for system actors)
- actor_type
- actor_id (optional)
- body
- created_at
- edited_at (optional)
- deleted_at (optional)
- metadata

The schema is illustrative rather than binding SQL. The invariant is that membership and visibility are first-class server-side data, not inferred from UI state.

---

6. Read State and Notifications

Ordinary conversation creates no Professionalism obligation.

Unread state exists for convenience, not status. The game must not reward rapid reading, rapid replies, message volume, streaks, online presence or other engagement metrics.

A per-member last-read marker may be used to derive unread conversation counts.

Notifications may distinguish:

- informational;
- social;
- action required;
- system.

Only an event that is already an authoritative game obligation may be labelled action required. A social message cannot create an obligation merely by being sent.

Notification preferences must be configurable. Muting a conversation must not suppress a separate authoritative game obligation attached to the same underlying game event.

---

7. Conversation Versus Game Action

Free text has no mechanical power.

Examples:

"Would you take £20m?" — conversation only.

"I accept." — conversation only.

Pressing the governed Submit Offer / Counter / Accept / Reject action — authoritative game action.

Where useful, the communication layer may render an authoritative event into the thread:

"Hamburg formally offered £20m."

That rendered line is a projection of canonical game state. It is not itself the transaction.

This rule applies equally to transfers, contracts, manager approaches, promises, registrations and any later interactive system.

---

8. Transfer and Recruitment Listings

Listings are first-class structured social objects rather than ephemeral chat messages.

Baseline listing types:

AVAILABLE — a club advertises a player for sale or loan.

WANTED — a club advertises a recruitment need.

VACANCY — an eligible managerial role is advertised where the Manager Career Constitution permits it.

MANAGER AVAILABLE — an eligible manager advertises availability where the Manager Career Constitution permits it.

Listings may contain structured filters and descriptive text. They may support discussion or private contact. A listing never constitutes a formal bid, offer, application or contract.

Listings expire or close explicitly and remain auditable where required by the Records or governance layer.

---

9. Privacy and Information Leakage

Private message content must never be used to create transfer rumours, player reactions, media stories, scouting knowledge, AI decisions or any other mechanical effect unless a future constitutional amendment explicitly authorises a narrowly defined use.

Rumour leakage continues to derive from logged game actions such as shortlisting, scouting, enquiries and bids under Information Part 3.

The system may know that a private conversation exists for delivery and security purposes. That fact alone has no game effect.

Private conversations, membership, read state and message content must never appear in unauthenticated feeds, public APIs, RSS, WebSub, rssCloud, public caches or public search indexes.

---

10. Public Feeds and RSS

RSS, Atom or JSON Feed may be exposed for information already public by constitutional rule.

Feeds are publication adapters, not the canonical communications database.

No communications feature may require RSS as its source of truth.

Public feed candidates may include world news, competition news, club news, public transfer listings and public recruitment listings.

Private conversations and private game workflows are never published as feeds.

---

11. Moderation and Safety

Managers must be able to report content. Private human-to-human communication must support blocking or equivalent protection without breaking authoritative game obligations.

Moderation actions that restrict, hide, suspend or remove content must be authenticated, auditable and governed.

A block may prevent ordinary direct social messages. It must not prevent delivery of an authoritative transfer response, sanction, competition notice or other required game event; those remain available through the structured system channel.

---

12. Retention and History

Not every message is part of permanent world history.

Canonical game events and records follow their owning Constitutions.

Social conversation retention is an implementation policy and must be published. Deletion or expiry of social messages must never delete or alter the authoritative game actions that may have been discussed alongside them.

Where a conversation contains system-rendered canonical events, the canonical source remains the game record even if the conversational projection later disappears.

---

13. Translation

The Constitution guarantees multilingual generated media. Human-to-human message translation is optional communication assistance, not an authoritative rewrite.

If machine translation of manager messages is introduced:

- the original text remains the source message;
- translated text is clearly presented as a translation;
- translation errors have no mechanical consequence;
- structured game actions use canonical structured values rather than translated prose.

---

14. Implementation Boundary

The existing TBG platform remains authoritative for identity, world membership, canonical objects, game actions, manager messages, notifications and public world-feed state.

The communications implementation should extend those existing systems rather than require a second identity store or convert TBG state into RSS as an intermediate authority.

Prior work from private Top 100 Chat is a reference implementation for:

- authenticated community access;
- stable manager-linked identity;
- server-side privacy boundaries;
- PWA delivery;
- opt-in Web Push lifecycle;
- safe object-to-conversation linking.

It is not itself the TBG communications datastore.

---

15. Initial Delivery Order

The implementation should proceed in bounded stages:

1. canonical conversation schema and RLS;
2. one-to-one manager conversations;
3. unread/read state;
4. manager-scoped notifications;
5. object binding;
6. public/scoped discussion unification with the existing World Feed;
7. transfer and recruitment listings;
8. links from conversations to authoritative structured actions;
9. optional public RSS/Atom/JSON Feed outputs;
10. later game-actor conversations where authorised.

Each stage must preserve the conversation/action boundary and may ship independently.

---

Golden Rule

The football world may talk about anything it is allowed to know. Talking about it does not make it true, official or binding.

Only the game decides.
