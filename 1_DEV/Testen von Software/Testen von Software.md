# Ordnerstruktur
Die Dateien mit den Testfällen sollten separat von dem eigentlichen Code abgelegt werden, da sie nicht zum ausgelieferten Code gehören. Z.B. Für Code "src/main/kotlin/..." und für Testfälle "src/test/kotlin/..."

# Von Testfall zu UnitTest
Ein Testfall führt nicht immer zu einem UnitTest. Ein Testfall kann zu mehreren UnitTests führen, da in jedem UnitTest nur ein einziger Aspekt untersucht werden soll.
