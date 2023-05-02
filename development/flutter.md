```dart
void main() {
  // var list = texts.cast()
  List<String> texts = ['roro', "fifi", "lolo"];
  Iterable<String> modifiedText = texts.map((text) => "$text huhu");
  print(modifiedText.toList());

  Map<String, String> bookMap = {};
//  texts.forEach((text) => book.addEntries({text: "content"}.entries));
  Iterable<bool> insertionSuccesses = texts.map((text) {
    bookMap.addEntries({text: "content"}.entries);
    return true;
  });
  //print(insertionSuccesses);
  print("Book map $bookMap");

  Map<String, String> bookFor = {};
  texts.forEach((text) {
    bookFor.addEntries({text: "content"}.entries);
  });

  print("Book for $bookFor");

  List<String> booksToString = bookFor.entries
      .toList()
      .map((entry) => "${entry.value} ${entry.key}")
      .toList();
  print(booksToString);

  bookFor.entries.map((entry) => "test").toList();
  // Map callback is not performed for all items at once if not calling
  // toList;
  // Map return an iterator which perform callback for current item
  // Printing the iterable will compute callback
  // Foreach perform callback
  // Var vs dynamic => var has its type set once for all at init
  // dynamic => type can change. if declare var but not set : defined as dynamic
  // Template string : "$var" => calls var.toString()

  Map<String, String> original = {'chapter1': "hello", 'chapter2': 'bonjour'};
  List<String> modified =
      original.entries.map((entry) => "${entry.value}").toList();
  print(modified);

  Map<String, Map<String, String>> magasin = {};
  Map<String, String> electro = {"console": "PS4", "tv": "Sony", "pc": "Mac"};
  Map<String, String> cuisine = {
    "four": "bosch",
    "induction": "continental",
    "frigo": "electrolux"
  };
  magasin.addEntries({"electro": electro}.entries);
  magasin["cuisine"] = cuisine;

  print(magasin);

  // Null checking is working using ?
  // Could also use containsKey
  print(magasin["electrod"]?["kiwa"] ?? "no electrod");
  print(magasin["electro"]?["console"] ?? "no kiwa");

  print(magasin.entries.map((rayon) =>
      "${rayon.key} does${rayon.value.containsValue("PS4") ? " " : " not "}contain a PS4"));

  Map<String, dynamic> json = {
    "glossary": {
      "title": "example glossary",
      "GlossDiv": {
        "titles": ["Science", "Human", "Health"],
        "GlossList": {
          "GlossEntry": {
            "ID": "SGML",
            "SortAs": "SGML",
            "GlossTerm": "Standard Generalized Markup Language",
            "Acronym": "SGML",
            "Abbrev": "ISO 8879:1986",
            "GlossDef": {
              "para":
                  "A meta-markup language, used to create markup languages such as DocBook.",
              "GlossSeeAlso": ["GML", "XML"]
            },
            "GlossSee": "markup"
          }
        }
      }
    }
  };
  
  // Casting map return value to use Iterable if needed
  // If storing int and double in array : inferred type will be num
  Iterable<String> ohTitles = json["glossary"]["GlossDiv"]["titles"].map<String>((title) => 2);
  print(ohTitles);
  // List.from <=> map().toList... No casting issue with List, no need to precast like for a map
  // Return value must match list template type
  List<String> ohTitlesList = List.from(ohTitles);
  print("ohTitlesList $ohTitlesList");
  
  List<String> ohTitlesFromListWoCasting = List.from(json["glossary"]["GlossDiv"]["titles"].map((title) => "$title oh"));
    print("ohTitlesFromListWoCasting $ohTitlesFromListWoCasting");

  
  print(json.entries.map((glossary) => glossary.value["GlossDiv"]["titles"].map((matter) => matter)).toList());
}

```
