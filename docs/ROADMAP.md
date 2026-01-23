# ROADMAP

Gevulot development roadmap. Features move from here to CHANGELOG when complete.

---

> 🤖
>
> [CHANGELOG](CHANGELOG.md) - What we did
> [ROADMAP](ROADMAP.md) - What we wanna do
> [CONTRIBUTING](CONTRIBUTING.md) - How we do it
> [CHECKS](CHECKS.md) - What we accept
>
> [/whatsup](../.github/prompts/whatsup.prompt.md) - The prompt that keeps us sane
>
> 🤖

---

### v0.1.0

#### Development Environment

Set up project foundation: language choice, tooling, hello world, and research literature.

- [ ] Choose tech stack (Flutter + Dart?)
- [ ] Development environment setup guide
- [ ] Hello World app (minimal iOS build)
- [ ] Research literature compilation (privacy, consent, distributed systems)
- [ ] Core dependencies decision (local storage, crypto, networking)

---

### v0.1.1

#### UX & Design Foundations

Define user flows and interaction patterns for consent-first contact management.

- [ ] User journey mapping (Me Card → Share → Update → Propagate)
- [ ] Wireframes for core screens
- [ ] Consent interaction patterns
- [ ] Visual design language (Gevulot identity)
- [ ] Prototype key flows (claim card, set permissions, share contact)

---

### v0.1.2

#### Security & Testing Strategy

Establish how to test Gevulot safely without compromising privacy or breaking trust.

- [ ] Threat model documentation
- [ ] Test data strategy (synthetic vs real contacts)
- [ ] Privacy-preserving testing approach
- [ ] Security audit checklist
- [ ] User testing protocol (consent, anonymization, data handling)
- [ ] Staging environment isolation

---

### v0.2.0

#### MVP - Core Contact Card

First working version with self-owned contact cards and basic propagation.

- [ ] iOS app scaffold (Flutter)
- [ ] "Me Card" claim flow
- [ ] Stable user ID generation
- [ ] Basic contact card CRUD
- [ ] Local storage setup

---

### v0.3.0

#### Group Permissions

Implement group-based visibility system.

- [ ] Group definitions (Close Friends, Family, Work, Grey Rock)
- [ ] Field-level permissions
- [ ] Move contacts between groups
- [ ] Visibility rules enforcement

---

### v0.4.0

#### Automatic Propagation

Enable real-time updates when contact cards change.

- [ ] Change detection system
- [ ] Permission-aware propagation
- [ ] Update notification system
- [ ] Conflict resolution

---

### v0.5.0

#### Multi-Platform Sync

Sync contacts across user's devices.

- [ ] Cloud backend (Firebase/Supabase)
- [ ] Multi-device sync
- [ ] Offline-first support
- [ ] Conflict resolution

---

## Future Ideas
