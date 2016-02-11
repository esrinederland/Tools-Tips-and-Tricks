# ---------------------------------------------------------------------------
# RunToolRun.py
# Usage: RunToolRun
# ---------------------------------------------------------------------------
# Import system modules
import sys, logging, datetime, importlib, arcpy

toolbox_pad = sys.argv[1]
toolbox_model = sys.argv[2]

# Local variables
vandaag = datetime.datetime.now().strftime("%Y%m%d%H%M%S")
logfile = toolbox_model + "_" + vandaag + ".log"
print "Logfile: " + logfile

# Initialize logging
logging.basicConfig(level=logging.DEBUG,format='%(asctime)s %(levelname)s %(message)s',filename=logfile,filemode='w')

try:
    # Laden van de toolbox (eventueel gerefereerde toolboxes worden automatisch meegeladen)...
    logging.info("Importeren toolbox: " + toolbox_pad)
    toolbox_alias = "mijnalias"
    arcpy.ImportToolbox(toolbox_pad,toolbox_alias)
    arcpy.OverWriteOutput = 1

    # Process: Model uitvoeren...
    logging.info("*** Uitvoeren model gestart *****************")

    # Ophalen juiste functie op basis van de parameters
    module = importlib.import_module('arcpy')
    function_name = toolbox_model + '_' + toolbox_alias

    logging.info("Starten functie: " + function_name)

    function = getattr(module, function_name)

    # Functie uitvoeren
    logging.info(sys.argv)
    if len(sys.argv) > 3:
        function(*sys.argv[3:])
    else:
        function()

    logging.info(arcpy.GetMessages(0))
    logging.info("SCRIPT SUCCESVOL AFGEROND")
except Exception as e:
    logging.error(str(sys.exc_info()[0]))
    logging.error(arcpy.GetMessages(0))
    logging.error("FOUT OPGETREDEN")


