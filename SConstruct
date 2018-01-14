import excons

env = excons.MakeBaseEnv()

include_qtpy = (excons.GetArgument("include-qtpy", 1, int) != 0)
include_contribs = (excons.GetArgument("include-contribs", 1, int) != 0)

version = "0.7.0"

pymods = ["opentimelineio", "opentimelineview"]
if include_qtpy:
   pymods += ["Qt/Qt.py"]

adapters = []
if include_contribs:
   adapters += excons.glob("contrib/adapters/*.*")

prjs = [
   {  "name": "OpenTimelineIO",
      "type": "install",
      "install": {
         "lib/python": pymods,
         "lib/contribs/adapters": adapters,
         "bin": excons.glob("bin/*")
      }
   }
]

excons.DeclareTargets(env, prjs)

outdir = excons.OutputBaseDirectory()

td = {"python": Glob(outdir + "/lib/python/*"),
      "bin":  Glob(outdir + "/bin/*")}

ecodirs = {"python": "/lib/python",
           "bin": "/bin"}

if include_contribs:
   td["contribs"] = Glob(outdir + "/lib/contribs/*")
   ecodirs["contribs"] = "/lib/contribs"

excons.EcosystemDist(env, "OpenTimelineIO.env", ecodirs, version=version, targets=td)

Default(["OpenTimelineIO"])
