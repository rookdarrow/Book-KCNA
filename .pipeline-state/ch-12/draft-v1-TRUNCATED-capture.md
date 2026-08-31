checks eliminate whole categories of cause before you spend an hour reading logs that were never going to contain the answer.

Bring three things with you from this chapter. The first is the shape of a Pod that was *rejected* rather than one that *failed* — you now know that admission can refuse an object outright, and that a refused object leaves nothing behind to inspect. The second is the `securityContext` fields, because a container that cannot write where it expects to write is a permissions failure wearing an application error's clothing. The third is Secrets: a Pod that references one that does not exist does not start, and it does not start in a specific, recognizable way.

You have spent twelve chapters learning what the cluster does when everything works. The next two are about the other case — and the honest truth is that the second kind of knowledge is what people actually get paid for.

---

🏆 **Safe Harbor**

That is Domain 2's security competency, complete. Nine sections, five independent systems, and one argument that took two chapters to set up.

Take stock of what changed. You can now look at any Kubernetes security control and say which of five questions it answers — *who are you*, *what may you do*, *what is stored where*, *what may your workload do to the machine*, *what did you ship* — and you can say which of the other four it does not answer, which is the harder and more useful half. You can derive the RBAC matrix rather than recalling it. You can look at a namespace's labels and a Pod's spec together and predict the outcome. And you can name the exposure path that no RBAC audit will show you.

The last one is worth sitting with for a moment. Most of what separates a competent Kubernetes engineer from a trusted one is not knowing more controls. It is knowing what each control does *not* cover, and refusing to be reassured by a green check mark that was measuring the wrong thing.

Chart, passage, dawn: 🗺️ → 🌊 → 🌅

> *"A grant says what it says. That is the whole design, and it is worth what it costs."*